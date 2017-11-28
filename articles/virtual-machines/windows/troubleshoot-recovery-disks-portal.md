---
title: "windows hello Azure 포털에서에서 VM을 문제 해결 aaaUse | Microsoft Docs"
description: "어떻게 연결 hello OS 디스크 tooa 복구 VM 사용 하 여 tootroubleshoot Windows 가상 컴퓨터 문제 Azure의 hello Azure 포털에 알아봅니다"
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
ms.openlocfilehash: 396f70338fa39f80bb9adcb9244d3c83f2a233eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-hello-azure-portal"></a><span data-ttu-id="e51c4-103">Windows VM hello OS 디스크 tooa 복구 VM을 연결 하 여 문제 해결 Azure 포털 hello를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e51c4-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using hello Azure portal</span></span>
<span data-ttu-id="e51c4-104">Azure에서 Windows 가상 컴퓨터 (VM) 부팅 또는 디스크 오류가 발생 하는 경우 문제 해결 단계는 자체 hello 가상 하드 디스크에서 tooperform을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="e51c4-105">일반적인 예로 hello VM 수 tooboot 성공적으로 않도록 방지 하는 실패 한 응용 프로그램 업데이트는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="e51c4-106">이 문서에 자세히 설명 방법 toouse hello Azure 포털 tooconnect 가상 하드 디스크 tooanother Windows VM toofix 오류를 다음 다시 원래 VM를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-106">This article details how toouse hello Azure portal tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>

## <a name="recovery-process-overview"></a><span data-ttu-id="e51c4-107">복구 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="e51c4-107">Recovery process overview</span></span>
<span data-ttu-id="e51c4-108">hello 문제 해결 과정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="e51c4-109">Hello VM 발생 문제, 유지 hello 가상 하드 디스크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="e51c4-110">첨부 하 고 문제 해결을 위해 hello 가상 하드 디스크 tooanother Windows VM에 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="e51c4-111">Toohello VM 문제 해결을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="e51c4-112">파일을 편집 하거나 hello 원래 가상 하드 디스크에서 다양 한 도구 toofix 문제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="e51c4-113">탑재 해제 하 고 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="e51c4-114">Hello 원래 가상 하드 디스크를 사용 하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-114">Create a VM using hello original virtual hard disk.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="e51c4-115">부팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="e51c4-115">Determine boot issues</span></span>
<span data-ttu-id="e51c4-116">VM 없는 이유 수 tooboot 올바르게 toodetermine hello 부트 진단이 VM 스크린샷을 검사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-116">toodetermine why your VM is not able tooboot correctly, examine hello boot diagnostics VM screenshot.</span></span> <span data-ttu-id="e51c4-117">일반적인 예로는 응용 프로그램 업데이트가 실패하거나 기본 가상 하드 디스크를 삭제 또는 이동하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-117">A common example would be a failed application update, or an underlying virtual hard disk being deleted or moved.</span></span>

<span data-ttu-id="e51c4-118">Hello 포털에서 VM을 선택 하 고 다음 toohello 아래쪽으로 스크롤하여 **지원 + 문제 해결** 섹션.</span><span class="sxs-lookup"><span data-stu-id="e51c4-118">Select your VM in hello portal and then scroll down toohello **Support + Troubleshooting** section.</span></span> <span data-ttu-id="e51c4-119">클릭 **진단 부팅** tooview hello 스크린 샷 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-119">Click **Boot diagnostics** tooview hello screenshot.</span></span> <span data-ttu-id="e51c4-120">특정 오류 메시지 또는 오류 코드에 유의 toohelp hello VM 문제 발생 이유를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-120">Note any specific error messages or error codes toohelp determine why hello VM is encountering an issue.</span></span> <span data-ttu-id="e51c4-121">hello 다음 예제에서 서비스를 중지 대기 VM:</span><span class="sxs-lookup"><span data-stu-id="e51c4-121">hello following example shows a VM waiting on stopping services:</span></span>

![VM 부팅 진단 콘솔 로그 보기](./media/troubleshoot-recovery-disks-portal/screenshot-error.png)

<span data-ttu-id="e51c4-123">클릭할 수도 있습니다 **스크린 샷** toodownload hello VM 스크린 샷 캡처.</span><span class="sxs-lookup"><span data-stu-id="e51c4-123">You can also click **Screenshot** toodownload a capture of hello VM screenshot.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="e51c4-124">기존 가상 하드 디스크 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="e51c4-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="e51c4-125">가상 하드 디스크 tooanother VM에 연결할 수 있습니다, 전에 hello 가상 하드 디스크 (VHD)의 tooidentify hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span> 

<span data-ttu-id="e51c4-126">Hello 포털에서 리소스 그룹을 선택 하 고 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-126">Select your resource group from hello portal, then select your storage account.</span></span> <span data-ttu-id="e51c4-127">클릭 **Blob**와 같이, 다음 예제는 hello:</span><span class="sxs-lookup"><span data-stu-id="e51c4-127">Click **Blobs**, as in hello following example:</span></span>

![저장소 Blob 선택](./media/troubleshoot-recovery-disks-portal/storage-account-overview.png)

<span data-ttu-id="e51c4-129">일반적으로 가상 하드 디스크를 저장하는 **vhd**로 명명된 컨테이너가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-129">Typically you have a container named **vhds** that stores your virtual hard disks.</span></span> <span data-ttu-id="e51c4-130">Hello 컨테이너 tooview 가상 하드 디스크의 목록을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-130">Select hello container tooview a list of virtual hard disks.</span></span> <span data-ttu-id="e51c4-131">VHD의 참고 hello 이름 (hello 접두사는 일반적으로 hello 이름 VM의):</span><span class="sxs-lookup"><span data-stu-id="e51c4-131">Note hello name of your VHD (hello prefix is usually hello name of your VM):</span></span>

![저장소 컨테이너에서 VHD 식별](./media/troubleshoot-recovery-disks-portal/storage-container.png)

<span data-ttu-id="e51c4-133">Hello 목록에서 기존 가상 하드 디스크를 선택 하 고 단계를 수행 하는 hello에 사용 하기 위해 hello URL을 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-133">Select your existing virtual hard disk from hello list and copy hello URL for use in hello following steps:</span></span>

![기존 가상 하드 디스크 URL 복사](./media/troubleshoot-recovery-disks-portal/copy-vhd-url.png)


## <a name="delete-existing-vm"></a><span data-ttu-id="e51c4-135">기존 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="e51c4-135">Delete existing VM</span></span>
<span data-ttu-id="e51c4-136">가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-136">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="e51c4-137">가상 하드 디스크는 자체 hello 운영 체제, 응용 프로그램 및 구성 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-137">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="e51c4-138">hello VM 자체 hello 크기 또는 위치를 정의 하 고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드 (NIC) 등의 리소스를 참조 하는 메타 데이터 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-138">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="e51c4-139">각 가상 하드 디스크에 연결 되어 있을 때 할당 한 임 대권을 tooa VM입니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-139">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="e51c4-140">데이터 디스크를 연결 하 고 hello VM에서 실행 중인 동안에 분리 수, 있지만 hello VM 리소스는 삭제 하지 않는 한 hello OS 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-140">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="e51c4-141">hello 임대는 해당 VM 중지 및 할당 취소 된 상태에 있을 경우에 tooassociate hello OS 디스크는 VM으로 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-141">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="e51c4-142">첫 번째 단계 toorecover hello VM은 자체 toodelete hello VM 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-142">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="e51c4-143">VM 삭제 hello 저장소 계정의 hello 가상 하드 디스크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-143">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="e51c4-144">VM을 삭제 하는 hello, 후 hello 가상 하드 디스크 tooanother VM tootroubleshoot 첨부 고 hello 오류를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-144">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="e51c4-145">Hello 포털에서 VM을 선택한 다음 클릭 **삭제**:</span><span class="sxs-lookup"><span data-stu-id="e51c4-145">Select your VM in hello portal, then click **Delete**:</span></span>

![부팅 오류를 보여 주는 VM 부팅 진단 스크린샷](./media/troubleshoot-recovery-disks-portal/stop-delete-vm.png)

<span data-ttu-id="e51c4-147">Hello VM가 hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 삭제를 마치기 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-147">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="e51c4-148">hello 임대 VM hello로 연결 하는 hello 가상 하드 디스크에 toobe hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-148">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="e51c4-149">기존 가상 하드 디스크 tooanother VM 연결</span><span class="sxs-lookup"><span data-stu-id="e51c4-149">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="e51c4-150">에 대 한 hello 다음 몇 단계 문제 해결을 위해 다른 VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-150">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="e51c4-151">Hello 기존 가상 하드 디스크 toothis VM toobe 수 toobrowse 문제 해결을 첨부 하 고이 정보를 hello 디스크의 콘텐츠를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-151">You attach hello existing virtual hard disk toothis troubleshooting VM toobe able toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="e51c4-152">이 프로세스 toocorrect를 통해 모든 구성 오류 또는 추가 응용 프로그램을 확인 또는 로그 파일, 예를 들어 시스템.</span><span class="sxs-lookup"><span data-stu-id="e51c4-152">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="e51c4-153">선택 하거나 문제 해결을 위해 다른 VM toouse 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-153">Choose or create another VM toouse for troubleshooting purposes.</span></span>

1. <span data-ttu-id="e51c4-154">Hello 포털에서 리소스 그룹을 선택 하 고 문제 해결 VM을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-154">Select your resource group from hello portal, then select your troubleshooting VM.</span></span> <span data-ttu-id="e51c4-155">**디스크**를 선택한 다음 **기존 연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-155">Select **Disks** and then click **Attach existing**:</span></span>

    ![Hello 포털에서 기존 디스크 연결](./media/troubleshoot-recovery-disks-portal/attach-existing-disk.png)

2. <span data-ttu-id="e51c4-157">tooselect 기존 가상 하드 디스크를 클릭 **VHD 파일**:</span><span class="sxs-lookup"><span data-stu-id="e51c4-157">tooselect your existing virtual hard disk, click **VHD File**:</span></span>

    ![기존 VHD 찾아보기](./media/troubleshoot-recovery-disks-portal/select-vhd-location.png)

3. <span data-ttu-id="e51c4-159">저장소 계정 및 컨테이너를 선택한 다음 기존 VHD를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-159">Select your storage account and container, then click your existing VHD.</span></span> <span data-ttu-id="e51c4-160">Hello 클릭 **선택** tooconfirm 선택한 단추:</span><span class="sxs-lookup"><span data-stu-id="e51c4-160">Click hello **Select** button tooconfirm your choice:</span></span>

    ![기존 VHD 선택](./media/troubleshoot-recovery-disks-portal/select-vhd.png)

4. <span data-ttu-id="e51c4-162">이제 선택한 VHD를 클릭 **확인** tooattach hello 기존 가상 하드 디스크:</span><span class="sxs-lookup"><span data-stu-id="e51c4-162">With your VHD now selected, click **OK** tooattach hello existing virtual hard disk:</span></span>

    ![기존 가상 하드 디스크 연결 확인](./media/troubleshoot-recovery-disks-portal/attach-disk-confirm.png)

5. <span data-ttu-id="e51c4-164">몇 초 후 hello **디스크** VM에 대 한 창에 데이터 디스크로 연결 된 기존 가상 하드 디스크를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-164">After a few seconds, hello **Disks** pane for your VM lists your existing virtual hard disk connected as a data disk:</span></span>

    ![데이터 디스크로 연결된 기존 가상 하드 디스크](./media/troubleshoot-recovery-disks-portal/attached-disk.png)


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="e51c4-166">Hello 연결 된 데이터 디스크를 탑재</span><span class="sxs-lookup"><span data-stu-id="e51c4-166">Mount hello attached data disk</span></span>

1. <span data-ttu-id="e51c4-167">원격 데스크톱 연결 tooyour VM을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-167">Open a Remote Desktop connection tooyour VM.</span></span> <span data-ttu-id="e51c4-168">Hello 포털에서 VM을 선택 하 고 클릭 **연결**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-168">Select your VM in hello portal and click **Connect**.</span></span> <span data-ttu-id="e51c4-169">다운로드 하 고 hello RDP 연결 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-169">Download and open hello RDP connection file.</span></span> <span data-ttu-id="e51c4-170">자격 증명 toolog tooyour VM에에서 다음과 같이 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-170">Enter your credentials toolog in tooyour VM as follows:</span></span>

    ![Tooyour 원격 데스크톱을 사용 하 여 VM에 로그인](./media/troubleshoot-recovery-disks-portal/open-remote-desktop.png)

2. <span data-ttu-id="e51c4-172">**서버 관리자**를 연 다음 **파일 및 저장소 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-172">Open **Server Manager**, then select **File and Storage Services**.</span></span> 

    ![서버 관리자에서 파일 및 저장소 서비스 선택](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

3. <span data-ttu-id="e51c4-174">hello 데이터 디스크가 자동으로 감지 되 고 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-174">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="e51c4-175">연결 된 디스크, 선택 toosee hello 목록이 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-175">toosee a list of hello connected disks, select **Disks**.</span></span> <span data-ttu-id="e51c4-176">사용자 데이터 디스크 tooview 볼륨 정보를 hello 드라이브 문자를 포함 하 여 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-176">You can select your data disk tooview volume information, including hello drive letter.</span></span> <span data-ttu-id="e51c4-177">다음 예제에서는 연결 된 데이터 디스크를 hello 및 사용 하 여 hello **f:**:</span><span class="sxs-lookup"><span data-stu-id="e51c4-177">hello following example shows hello data disk attached and using **F:**:</span></span>

    ![서버 관리자의 연결된 디스크 및 볼륨 정보](./media/troubleshoot-recovery-disks-portal/server-manager-disk-attached.png)


## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="e51c4-179">원래 가상 하드 디스크의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="e51c4-179">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="e51c4-180">이제 hello 기존 가상 하드 디스크를 탑재, 모든 유지 관리 및 문제 해결 단계는 필요에 따라 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-180">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="e51c4-181">Hello 문제를 해결 한 후 단계를 수행 하는 hello로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-181">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="e51c4-182">원래 가상 하드 디스크의 탑재 해제 및 분리</span><span class="sxs-lookup"><span data-stu-id="e51c4-182">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="e51c4-183">프로그램 오류가 해결 되 면 hello 기존 가상 하드 디스크 문제 해결 VM에서 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-183">Once your errors are resolved, detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="e51c4-184">VM의 문제를 해결 하는 hello 가상 하드 디스크 toohello 연결 hello 임대가 해제 될 때까지 다른 VM과 가상 하드 디스크를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-184">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="e51c4-185">Hello RDP 세션 tooyour VM에서에서 열고 **서버 관리자**을 선택한 후 **파일 및 저장소 서비스**:</span><span class="sxs-lookup"><span data-stu-id="e51c4-185">From hello RDP session tooyour VM, open **Server Manager**, then select **File and Storage Services**:</span></span>

    ![서버 관리자에서 파일 및 저장소 서비스 선택](./media/troubleshoot-recovery-disks-portal/server-manager-select-storage.png)

2. <span data-ttu-id="e51c4-187">**디스크**를 선택한 다음 데이터 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-187">Select **Disks** and then select your data disk.</span></span> <span data-ttu-id="e51c4-188">데이터 디스크를 마우스 오른쪽 단추로 클릭하고 **오프라인 상태로 전환**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-188">Right-click on your data disk and select **Take Offline**:</span></span>

    ![서버 관리자에서 오프 라인으로 hello 데이터 디스크 설정](./media/troubleshoot-recovery-disks-portal/server-manager-set-disk-offline.png)

3. <span data-ttu-id="e51c4-190">이제 hello hello VM에서에서 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-190">Now detach hello virtual hard disk from hello VM.</span></span> <span data-ttu-id="e51c4-191">Hello Azure 포털에서에서 VM을 선택 하 고 클릭 **디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-191">Select your VM in hello Azure portal and click **Disks**.</span></span> <span data-ttu-id="e51c4-192">기존 가상 하드 디스크를 선택한 다음 **분리**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-192">Select your existing virtual hard disk and then click **Detach**:</span></span>

    ![기존 가상 하드 디스크 분리](./media/troubleshoot-recovery-disks-portal/detach-disk.png)

    <span data-ttu-id="e51c4-194">계속 하기 전에 VM hello hello 데이터 디스크를 성공적으로 분리 된 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-194">Wait until hello VM has successfully detached hello data disk before continuing.</span></span>

## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="e51c4-195">원래 하드 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="e51c4-195">Create VM from original hard disk</span></span>
<span data-ttu-id="e51c4-196">원래 가상 하드 디스크에서 VM에서 사용할 toocreate [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-196">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="e51c4-197">hello에서 VHD URL hello를 사용 하 여 기존 가상 네트워크를으로 VM을 배포 하는 hello 템플릿 이전 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-197">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="e51c4-198">Hello 클릭 **tooAzure 배포** 다음과 같이 단추:</span><span class="sxs-lookup"><span data-stu-id="e51c4-198">Click hello **Deploy tooAzure** button as follows:</span></span>

![GitHub의 템플릿에서 VM 배포](./media/troubleshoot-recovery-disks-portal/deploy-template-from-github.png)

<span data-ttu-id="e51c4-200">hello 템플릿 배포에 대 한 Azure 포털 hello에 로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-200">hello template is loaded into hello Azure portal for deployment.</span></span> <span data-ttu-id="e51c4-201">새 VM 및 기존 Azure 리소스에 대 한 hello 이름을 입력 하 고 hello URL tooyour 기존 가상 하드 디스크를 붙여 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-201">Enter hello names for your new VM and existing Azure resources, and paste hello URL tooyour existing virtual hard disk.</span></span> <span data-ttu-id="e51c4-202">toobegin hello 배포 클릭 **구매**:</span><span class="sxs-lookup"><span data-stu-id="e51c4-202">toobegin hello deployment, click **Purchase**:</span></span>

![템플릿에서 VM 배포](./media/troubleshoot-recovery-disks-portal/deploy-from-image.png)


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="e51c4-204">부트 진단 다시 사용</span><span class="sxs-lookup"><span data-stu-id="e51c4-204">Re-enable boot diagnostics</span></span>
<span data-ttu-id="e51c4-205">Hello 기존 가상 하드 디스크에서 VM을 만들 때 부트 진단이 자동으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-205">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="e51c4-206">toocheck 부트 진단의 상태를 hello 및 hello 포털에서 VM을 선택 합니다. 필요한 경우 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-206">toocheck hello status of boot diagnostics and turn on if needed, select your VM in hello portal.</span></span> <span data-ttu-id="e51c4-207">**모니터링**에서 **진단 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-207">Under **Monitoring**, click **Diagnostics settings**.</span></span> <span data-ttu-id="e51c4-208">Hello 상태는 확인 **에**, 너무 확인 표시를 다음 hello 및**진단 부팅** 을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-208">Ensure hello status is **On**, and hello check mark next too**Boot diagnostics** is selected.</span></span> <span data-ttu-id="e51c4-209">항목을 변경하려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-209">If you make any changes, click **Save**:</span></span>

![부팅 진단 설정 업데이트](./media/troubleshoot-recovery-disks-portal/reenable-boot-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="e51c4-211">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e51c4-211">Next steps</span></span>
<span data-ttu-id="e51c4-212">Tooyour VM을 연결 하는 데 문제가 있는 경우 참조 [문제를 해결 하는 RDP 연결 tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="e51c4-212">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="e51c4-213">VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Windows VM에서 응용 프로그램 연결 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e51c4-213">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="e51c4-214">Resource Manager를 사용하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e51c4-214">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>