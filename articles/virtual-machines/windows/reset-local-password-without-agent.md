---
title: "Azure 에이전트 없이 로컬 Windows 암호 aaaReset | Microsoft Docs"
description: "Hello Azure 게스트 에이전트가 설치 되어 있지 않거나 VM에서 올바르게 작동 하는 경우 로컬 Windows 사용자 계정의 암호 tooreset hello 하는 방법"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a><span data-ttu-id="8abe4-103">어떻게 tooreset Azure VM에 대 한 로컬 Windows 암호</span><span class="sxs-lookup"><span data-stu-id="8abe4-103">How tooreset local Windows password for Azure VM</span></span>
<span data-ttu-id="8abe4-104">Hello hello를 사용 하 여 Azure에서 VM의 로컬 Windows 암호를 다시 설정할 수 있습니다 [Azure 포털 또는 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello Azure 게스트 에이전트가 설치 되어 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-104">You can reset hello local Windows password of a VM in Azure using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided hello Azure guest agent is installed.</span></span> <span data-ttu-id="8abe4-105">이 메서드는 기본 방법 tooreset hello Azure VM에 대 한 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-105">This method is hello primary way tooreset a password for an Azure VM.</span></span> <span data-ttu-id="8abe4-106">Hello Azure 게스트 에이전트가 응답 하지 않거나 사용자 지정 이미지를 업로드 한 후 tooinstall 실패 된 문제를 발생 하는 경우 Windows 암호를 수동으로 다시 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-106">If you encounter issues with hello Azure guest agent not responding, or failing tooinstall after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="8abe4-107">이 문서 tooreset 로컬 계정 암호를 연결 하 여 운영 체제 원본 가상 디스크 tooanother VM hello 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-107">This article details how tooreset a local account password by attaching hello source OS virtual disk tooanother VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="8abe4-108">이 프로세스는 마지막 수단으로만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-108">Only use this process as a last resort.</span></span> <span data-ttu-id="8abe4-109">항상 tooreset hello를 사용 하 여 암호를 시도 [Azure 포털 또는 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 첫 번째입니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-109">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-hello-process"></a><span data-ttu-id="8abe4-110">Hello 프로세스의 개요</span><span class="sxs-lookup"><span data-stu-id="8abe4-110">Overview of hello process</span></span>
<span data-ttu-id="8abe4-111">로컬 암호 액세스 toohello Azure 게스트 에이전트가 때 Azure에서 Windows VM에 대 한 재설정을 수행 하기 위한 hello 핵심 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-111">hello core steps for performing a local password reset for a Windows VM in Azure when there is no access toohello Azure guest agent is as follows:</span></span>

* <span data-ttu-id="8abe4-112">Hello 원본 VM을 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-112">Delete hello source VM.</span></span> <span data-ttu-id="8abe4-113">hello 가상 디스크에 그대로 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-113">hello virtual disks are retained.</span></span>
* <span data-ttu-id="8abe4-114">Hello에 hello 소스 VM의 OS 디스크 tooanother VM 연결 Azure 구독 내에서 같은 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-114">Attach hello source VM's OS disk tooanother VM on hello same location within your Azure subscription.</span></span> <span data-ttu-id="8abe4-115">이 VM은 참조 tooas hello VM 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-115">This VM is referred tooas hello troubleshooting VM.</span></span>
* <span data-ttu-id="8abe4-116">VM의 문제를 해결 하는 hello를 사용 하 여 hello 소스 VM의 OS 디스크에 일부 구성 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-116">Using hello troubleshooting VM, create some config files on hello source VM's OS disk.</span></span>
* <span data-ttu-id="8abe4-117">VM의 문제를 해결 하는 hello에서 hello VM의 OS 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-117">Detach hello VM's OS disk from hello troubleshooting VM.</span></span>
* <span data-ttu-id="8abe4-118">리소스 관리자 템플릿 toocreate hello 원래 가상 디스크를 사용 하 여 VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-118">Use a Resource Manager template toocreate a VM, using hello original virtual disk.</span></span>
* <span data-ttu-id="8abe4-119">Hello 새 VM 부팅을 hello config 파일 때 필요한 hello 사용자의 hello 암호를 업데이트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-119">When hello new VM boots, hello config files you create update hello password of hello required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="8abe4-120">자세한 단계</span><span class="sxs-lookup"><span data-stu-id="8abe4-120">Detailed steps</span></span>
<span data-ttu-id="8abe4-121">항상 tooreset hello를 사용 하 여 암호를 시도 [Azure 포털 또는 Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) hello 다음 단계를 시도 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="8abe4-121">Always try tooreset a password using hello [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying hello following steps.</span></span> <span data-ttu-id="8abe4-122">시작하기 전에 VM을 백업했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="8abe4-123">삭제 hello Azure 포털에서 VM의 영향을 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-123">Delete hello affected VM in Azure portal.</span></span> <span data-ttu-id="8abe4-124">VM 삭제 hello만 hello Azure 내에서 VM의 hello 참조 hello 메타 데이터를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-124">Deleting hello VM only deletes hello metadata, hello reference of hello VM within Azure.</span></span> <span data-ttu-id="8abe4-125">hello 가상 디스크는 hello VM 삭제 될 때 유지 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-125">hello virtual disks are retained when hello VM is deleted:</span></span>
   
   * <span data-ttu-id="8abe4-126">Hello Azure 포털에에서 선택 hello VM 클릭 *삭제*:</span><span class="sxs-lookup"><span data-stu-id="8abe4-126">Select hello VM in hello Azure portal, click *Delete*:</span></span>
     
     ![기존 VM 삭제](./media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="8abe4-128">Hello 소스 VM의 OS 디스크 toohello VM 문제 해결을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-128">Attach hello source VM’s OS disk toohello troubleshooting VM.</span></span> <span data-ttu-id="8abe4-129">VM의 문제를 해결 하는 hello hello에 있어야 합니다. hello 소스 VM의 OS 디스크와 동일한 지역 (예: `West US`):</span><span class="sxs-lookup"><span data-stu-id="8abe4-129">hello troubleshooting VM must be in hello same region as hello source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="8abe4-130">Hello hello Azure 포털에서에서 VM을 문제 해결을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-130">Select hello troubleshooting VM in hello Azure portal.</span></span> <span data-ttu-id="8abe4-131">*디스크* | *기존 연결*을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![기존 디스크 연결](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="8abe4-133">선택 *VHD 파일* 한 후 원본 VM을 포함 하는 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-133">Select *VHD File* and then select hello storage account that contains your source VM:</span></span>
     
     ![저장소 계정 선택](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     <span data-ttu-id="8abe4-135">Hello 소스 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-135">Select hello source container.</span></span> <span data-ttu-id="8abe4-136">hello 원본 컨테이너는 일반적으로 *vhd*:</span><span class="sxs-lookup"><span data-stu-id="8abe4-136">hello source container is typically *vhds*:</span></span>
     
     ![저장소 컨테이너 선택](./media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="8abe4-138">운영 체제 vhd tooattach hello를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-138">Select hello OS vhd tooattach.</span></span> <span data-ttu-id="8abe4-139">클릭 *선택* toocomplete hello 프로세스:</span><span class="sxs-lookup"><span data-stu-id="8abe4-139">Click *Select* toocomplete hello process:</span></span>
     
     ![원본 가상 디스크 선택](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="8abe4-141">원격 데스크톱을 사용 하 여 VM을 문제 해결 toohello를 연결 하 고 hello 소스 VM의 OS 디스크가 표시:</span><span class="sxs-lookup"><span data-stu-id="8abe4-141">Connect toohello troubleshooting VM using Remote Desktop and ensure hello source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="8abe4-142">Hello hello Azure 포털에서에서 VM을 문제 해결을 선택 하 고 클릭 *연결*합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-142">Select hello troubleshooting VM in hello Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="8abe4-143">다운로드 하는 hello RDP 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-143">Open hello RDP file that downloads.</span></span> <span data-ttu-id="8abe4-144">Hello 사용자 이름 및 VM 문제를 해결 하는 hello의 암호를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-144">Enter hello username and password of hello troubleshooting VM.</span></span>
   * <span data-ttu-id="8abe4-145">파일 탐색기에서 연결 하는 hello 데이터 디스크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-145">In File Explorer, look for hello data disk you attached.</span></span> <span data-ttu-id="8abe4-146">Hello VM의 VHD가 소스 hello VM 문제를 해결 하는 유일한 데이터 연결 된 디스크 toohello, hello f: 드라이브가 상태 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-146">If hello source VM’s VHD is hello only data disk attached toohello troubleshooting VM, it should be hello F: drive:</span></span>
     
     ![연결된 데이터 디스크 보기](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="8abe4-148">만들 `gpt.ini` 에 `\Windows\System32\GroupPolicy` hello 소스 VM의 드라이브에 있음 (gpt.ini 있으면 이름을 toogpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="8abe4-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on hello source VM’s drive (if gpt.ini exists, rename toogpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="8abe4-149">않는 실수로 C:\Windows에 있는 파일을 다음 hello 만들 하 hello hello VM 문제 해결에 대 한 운영 체제 드라이브에 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-149">Make sure that you do not accidentally create hello following files in C:\Windows, hello OS drive for hello troubleshooting VM.</span></span> <span data-ttu-id="8abe4-150">Hello 다음 원본에 데이터 디스크로 연결 된 VM에 대 한 hello 운영 체제 드라이브에 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-150">Create hello following files in hello OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="8abe4-151">Hello에 줄을 다음 hello 추가 `gpt.ini` 만든 파일:</span><span class="sxs-lookup"><span data-stu-id="8abe4-151">Add hello following lines into hello `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![gpt.ini 만들기](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="8abe4-153">`\Windows\System32\GroupPolicy\Machine\Scripts`에 `scripts.ini`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="8abe4-154">숨겨진 폴더가 표시되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="8abe4-155">필요한 경우 만들 hello `Machine` 또는 `Scripts` 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-155">If needed, create hello `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="8abe4-156">다음 줄 hello hello 추가 `scripts.ini` 만든 파일:</span><span class="sxs-lookup"><span data-stu-id="8abe4-156">Add hello following lines hello `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![scripts.ini 만들기](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="8abe4-158">만들기 `FixAzureVM.cmd` 에 `\Windows\System32` 내용 뒤, 대체 hello로 `<username>` 및 `<newpassword>` 고유한 값으로.</span><span class="sxs-lookup"><span data-stu-id="8abe4-158">Create `FixAzureVM.cmd` in `\Windows\System32` with hello following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![FixAzureVM.cmd 만들기](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="8abe4-160">Hello 새 암호를 정의 하는 경우에 VM에 대 한 암호 복잡성 요구 사항을 구성 하는 hello를 충족 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-160">You must meet hello configured password complexity requirements for your VM when defining hello new password.</span></span>
7. <span data-ttu-id="8abe4-161">Azure 포털에서 VM의 문제를 해결 하는 hello에서 hello 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-161">In Azure portal, detach hello disk from hello troubleshooting VM:</span></span>
   
   * <span data-ttu-id="8abe4-162">Hello Azure 포털에서에서 VM 문제를 해결 하는 hello 선택를 클릭 *디스크*합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-162">Select hello troubleshooting VM in hello Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="8abe4-163">2 단계에서 연결 된 선택 hello 데이터 디스크를 클릭 *분리*:</span><span class="sxs-lookup"><span data-stu-id="8abe4-163">Select hello data disk attached in step 2, click *Detach*:</span></span>
     
     ![디스크 분리](./media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="8abe4-165">VM을 만들기 전에 hello URI tooyour 소스 OS 디스크를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-165">Before you create a VM, obtain hello URI tooyour source OS disk:</span></span>
   
   * <span data-ttu-id="8abe4-166">Hello Azure 포털에서에서 저장소 계정을 선택 hello 클릭 *Blob*합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-166">Select hello storage account in hello Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="8abe4-167">Hello 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-167">Select hello container.</span></span> <span data-ttu-id="8abe4-168">hello 원본 컨테이너는 일반적으로 *vhd*:</span><span class="sxs-lookup"><span data-stu-id="8abe4-168">hello source container is typically *vhds*:</span></span>
     
     ![저장소 계정 Blob 선택](./media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="8abe4-170">소스 VM OS VHD를 선택 하 고 hello 클릭 *복사* 단추 다음 toohello *URL* 이름:</span><span class="sxs-lookup"><span data-stu-id="8abe4-170">Select your source VM OS VHD and click hello *Copy* button next toohello *URL* name:</span></span>
     
     ![디스크 URI 복사](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="8abe4-172">Hello 소스 VM의 OS 디스크에서 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-172">Create a VM from hello source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="8abe4-173">사용 하 여 [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate 특수 VHD에서 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate a VM from a specialized VHD.</span></span> <span data-ttu-id="8abe4-174">Hello 클릭 `Deploy tooAzure` 단추 tooopen hello Azure 포털 hello 템플릿 기반 세부 정보가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-174">Click hello `Deploy tooAzure` button tooopen hello Azure portal with hello templated details populated for you.</span></span>
   * <span data-ttu-id="8abe4-175">Hello VM에 대 한 모든 hello 이전 설정을 tooretain 하려는 경우 선택 *템플릿 편집* tooprovide 기존 VNet, 서브넷, 네트워크 어댑터 또는 공용 IP입니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-175">If you want tooretain all hello previous settings for hello VM, select *Edit template* tooprovide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="8abe4-176">Hello에 `OSDISKVHDURI` 매개 변수 텍스트 상자, 붙여넣기 hello hello 앞 단계에서에서 원본 VHD의 URI를 가져올:</span><span class="sxs-lookup"><span data-stu-id="8abe4-176">In hello `OSDISKVHDURI` parameter text box, paste hello URI of your source VHD obtain in hello preceding step:</span></span>
     
     ![템플릿에서 VM 만들기](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="8abe4-178">새 VM에서 실행 되 고 hello, 후 toohello hello 새 암호로 hello에 지정 된 원격 데스크톱을 사용 하 여 VM을 연결 `FixAzureVM.cmd` 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-178">After hello new VM is running, connect toohello VM using Remote Desktop with hello new password you specified in hello `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="8abe4-179">원격 세션 toohello에서 새 VM을 따라 제거 hello hello 환 tooclean 파일:</span><span class="sxs-lookup"><span data-stu-id="8abe4-179">From your remote session toohello new VM, remove hello following files tooclean up hello environment:</span></span>
    
    * <span data-ttu-id="8abe4-180">%windir%\System32에서</span><span class="sxs-lookup"><span data-stu-id="8abe4-180">From %windir%\System32</span></span>
      * <span data-ttu-id="8abe4-181">FixAzureVM.cmd 제거</span><span class="sxs-lookup"><span data-stu-id="8abe4-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="8abe4-182">%windir%\System32\GroupPolicy\Machine\에서</span><span class="sxs-lookup"><span data-stu-id="8abe4-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="8abe4-183">scripts.ini 제거</span><span class="sxs-lookup"><span data-stu-id="8abe4-183">remove scripts.ini</span></span>
    * <span data-ttu-id="8abe4-184">%windir%\System32\GroupPolicy에서</span><span class="sxs-lookup"><span data-stu-id="8abe4-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="8abe4-185">(gpt.ini, 전에 있으며 toogpt.ini.bak, 이름 바꾸기 hello.bak 파일 백 toogpt.ini 바꾼) 경우 gpt.ini 제거</span><span class="sxs-lookup"><span data-stu-id="8abe4-185">remove gpt.ini (if gpt.ini existed before, and you renamed it toogpt.ini.bak, rename hello .bak file back toogpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="8abe4-186">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8abe4-186">Next steps</span></span>
<span data-ttu-id="8abe4-187">원격 데스크톱을 사용 하 여 계속 연결할 수 없는 경우 참조 hello [RDP 문제 해결 가이드](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-187">If you still cannot connect using Remote Desktop, see hello [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="8abe4-188">hello [자세한 문제 해결 가이드 RDP](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) 특정 단계를 사용 하지 않고 메서드 문제 해결을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-188">hello [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="8abe4-189">직접적인 도움을 위해 [Azure 지원 요청](https://azure.microsoft.com/support/options/)을 개설할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8abe4-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>

