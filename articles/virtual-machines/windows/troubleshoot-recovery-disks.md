---
title: "windows Azure PowerShell을 사용 하 여 VM을 문제 해결 aaaUse | Microsoft Docs"
description: "Windows VM tootroubleshoot Azure의 hello OS 디스크 tooa 복구 Azure PowerShell을 사용 하 여 VM을 연결 하 여 발급 하는 방법을 알아봅니다"
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
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a><span data-ttu-id="b4600-103">Windows VM hello OS 디스크 tooa 복구 Azure PowerShell을 사용 하 여 VM을 연결 하 여 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b4600-103">Troubleshoot a Windows VM by attaching hello OS disk tooa recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="b4600-104">Azure에서 Windows 가상 컴퓨터 (VM) 부팅 또는 디스크 오류가 발생 하는 경우 문제 해결 단계는 자체 hello 가상 하드 디스크에서 tooperform을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need tooperform troubleshooting steps on hello virtual hard disk itself.</span></span> <span data-ttu-id="b4600-105">일반적인 예로 hello VM 수 tooboot 성공적으로 않도록 방지 하는 실패 한 응용 프로그램 업데이트는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-105">A common example would be a failed application update that prevents hello VM from being able tooboot successfully.</span></span> <span data-ttu-id="b4600-106">이 세부 정보를 어떻게 문서 toouse Azure PowerShell tooconnect에 가상 하드 디스크 tooanother Windows VM toofix 오류를 다시 만들어야 원래 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-106">This article details how toouse Azure PowerShell tooconnect your virtual hard disk tooanother Windows VM toofix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="b4600-107">복구 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="b4600-107">Recovery process overview</span></span>
<span data-ttu-id="b4600-108">hello 문제 해결 과정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-108">hello troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="b4600-109">Hello VM 발생 문제, 유지 hello 가상 하드 디스크를 삭제 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-109">Delete hello VM encountering issues, keeping hello virtual hard disks.</span></span>
2. <span data-ttu-id="b4600-110">첨부 하 고 문제 해결을 위해 hello 가상 하드 디스크 tooanother Windows VM에 탑재 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-110">Attach and mount hello virtual hard disk tooanother Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="b4600-111">Toohello VM 문제 해결을 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-111">Connect toohello troubleshooting VM.</span></span> <span data-ttu-id="b4600-112">파일을 편집 하거나 hello 원래 가상 하드 디스크에서 다양 한 도구 toofix 문제를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-112">Edit files or run any tools toofix issues on hello original virtual hard disk.</span></span>
4. <span data-ttu-id="b4600-113">탑재 해제 하 고 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-113">Unmount and detach hello virtual hard disk from hello troubleshooting VM.</span></span>
5. <span data-ttu-id="b4600-114">Hello 원래 가상 하드 디스크를 사용 하는 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-114">Create a VM using hello original virtual hard disk.</span></span>

<span data-ttu-id="b4600-115">확인 했는지 [최신 Azure PowerShell hello](/powershell/azure/overview) 설치 하 고 tooyour 구독에 기록:</span><span class="sxs-lookup"><span data-stu-id="b4600-115">Make sure that you have [hello latest Azure PowerShell](/powershell/azure/overview) installed and logged in tooyour subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="b4600-116">Hello 다음 예에서는 매개 변수 이름은 고유한 값으로 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-116">In hello following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="b4600-117">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="b4600-118">부팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="b4600-118">Determine boot issues</span></span>
<span data-ttu-id="b4600-119">Azure에서 VM의 스크린샷을 볼 수 있습니다 toohelp 부팅 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-119">You can view a screenshot of your VM in Azure toohelp troubleshoot boot issues.</span></span> <span data-ttu-id="b4600-120">이 스크린 샷 VM tooboot 실패 이유를 파악 하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-120">This screenshot can help identify why a VM fails tooboot.</span></span> <span data-ttu-id="b4600-121">hello 다음 예제에서는 가져옵니다 hello 스크린 샷 hello 라는 Windows VM에서에서 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4600-121">hello following example gets hello screenshot from hello Windows VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="b4600-122">Hello 스크린 샷 toodetermine hello VM tooboot를 실패 한 이유를 검토 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-122">Review hello screenshot toodetermine why hello VM is failing tooboot.</span></span> <span data-ttu-id="b4600-123">제공된 특정 오류 메시지 또는 오류 코드를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="b4600-124">기존 가상 하드 디스크 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="b4600-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="b4600-125">가상 하드 디스크 tooanother VM에 연결할 수 있습니다, 전에 hello 가상 하드 디스크 (VHD)의 tooidentify hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-125">Before you can attach your virtual hard disk tooanother VM, you need tooidentify hello name of hello virtual hard disk (VHD).</span></span>

<span data-ttu-id="b4600-126">hello 다음 예제에서는 가져옵니다 hello 라는 VM에 대 한 정보 `myVM` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4600-126">hello following example gets information for hello VM named `myVM` in hello resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="b4600-127">검색할 `Vhd URI` hello 내 `StorageProfile` hello 출력에서 hello 명령 앞의 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-127">Look for `Vhd URI` within hello `StorageProfile` section from hello output of hello preceding command.</span></span> <span data-ttu-id="b4600-128">hello 다음 잘린된 예제는 출력 hello `Vhd URI` hello 코드 블록의 hello 끝 쪽으로:</span><span class="sxs-lookup"><span data-stu-id="b4600-128">hello following truncated example output shows hello `Vhd URI` towards hello end of hello code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="b4600-129">기존 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="b4600-129">Delete existing VM</span></span>
<span data-ttu-id="b4600-130">가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="b4600-131">가상 하드 디스크는 자체 hello 운영 체제, 응용 프로그램 및 구성 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-131">A virtual hard disk is where hello operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="b4600-132">hello VM 자체 hello 크기 또는 위치를 정의 하 고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드 (NIC) 등의 리소스를 참조 하는 메타 데이터 일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-132">hello VM itself is just metadata that defines hello size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="b4600-133">각 가상 하드 디스크에 연결 되어 있을 때 할당 한 임 대권을 tooa VM입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-133">Each virtual hard disk has a lease assigned when attached tooa VM.</span></span> <span data-ttu-id="b4600-134">데이터 디스크를 연결 하 고 hello VM에서 실행 중인 동안에 분리 수, 있지만 hello VM 리소스는 삭제 하지 않는 한 hello OS 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-134">Although data disks can be attached and detached even while hello VM is running, hello OS disk cannot be detached unless hello VM resource is deleted.</span></span> <span data-ttu-id="b4600-135">hello 임대는 해당 VM 중지 및 할당 취소 된 상태에 있을 경우에 tooassociate hello OS 디스크는 VM으로 계속 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-135">hello lease continues tooassociate hello OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="b4600-136">첫 번째 단계 toorecover hello VM은 자체 toodelete hello VM 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-136">hello first step toorecover your VM is toodelete hello VM resource itself.</span></span> <span data-ttu-id="b4600-137">VM 삭제 hello 저장소 계정의 hello 가상 하드 디스크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-137">Deleting hello VM leaves hello virtual hard disks in your storage account.</span></span> <span data-ttu-id="b4600-138">VM을 삭제 하는 hello, 후 hello 가상 하드 디스크 tooanother VM tootroubleshoot 첨부 고 hello 오류를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-138">After hello VM is deleted, you attach hello virtual hard disk tooanother VM tootroubleshoot and resolve hello errors.</span></span>

<span data-ttu-id="b4600-139">다음 예에서는 삭제 하는 hello hello 라는 VM `myVM` 이라는 hello 리소스 그룹에서 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4600-139">hello following example deletes hello VM named `myVM` from hello resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="b4600-140">Hello VM가 hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 삭제를 마치기 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-140">Wait until hello VM has finished deleting before you attach hello virtual hard disk tooanother VM.</span></span> <span data-ttu-id="b4600-141">hello 임대 VM hello로 연결 하는 hello 가상 하드 디스크에 toobe hello 가상 하드 디스크 tooanother VM을 연결 하기 전에 해제 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-141">hello lease on hello virtual hard disk that associates it with hello VM needs toobe released before you can attach hello virtual hard disk tooanother VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a><span data-ttu-id="b4600-142">기존 가상 하드 디스크 tooanother VM 연결</span><span class="sxs-lookup"><span data-stu-id="b4600-142">Attach existing virtual hard disk tooanother VM</span></span>
<span data-ttu-id="b4600-143">에 대 한 hello 다음 몇 단계 문제 해결을 위해 다른 VM을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-143">For hello next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="b4600-144">Hello 기존 가상 하드 디스크 toothis VM toobrowse 문제 해결을 첨부 하 고이 정보를 hello 디스크의 콘텐츠를 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-144">You attach hello existing virtual hard disk toothis troubleshooting VM toobrowse and edit hello disk's content.</span></span> <span data-ttu-id="b4600-145">이 프로세스 toocorrect를 통해 모든 구성 오류 또는 추가 응용 프로그램을 확인 또는 로그 파일, 예를 들어 시스템.</span><span class="sxs-lookup"><span data-stu-id="b4600-145">This process allows you toocorrect any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="b4600-146">선택 하거나 문제 해결을 위해 다른 VM toouse 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-146">Choose or create another VM toouse for troubleshooting purposes.</span></span>

<span data-ttu-id="b4600-147">Hello 기존 가상 하드 디스크를 연결할 경우 hello 앞에서 만든 hello URL toohello 디스크 지정 `Get-AzureRmVM` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-147">When you attach hello existing virtual hard disk, specify hello URL toohello disk obtained in hello preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="b4600-148">hello 다음 예제에서는 연결 가상 컴퓨터 V 문제를 해결 하는 기존 가상 하드 디스크 toohello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4600-148">hello following example attaches an existing virtual hard disk toohello troubleshooting VM named `myVMRecovery` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="b4600-149">디스크 추가 hello 디스크의 toospecify hello 크기가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-149">Adding a disk requires you toospecify hello size of hello disk.</span></span> <span data-ttu-id="b4600-150">기존 디스크를 연결 했습니다 hello `-DiskSizeInGB` 로 지정 된 `$null`합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-150">As we attach an existing disk, hello `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="b4600-151">이 값을 입력 하면 hello 데이터 디스크가 올바르게 연결 되었는지, 및 hello 하지 않고 필요한 toodetermine hello 데이터 디스크의 실제 크기입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-151">This value ensures hello data disk is correctly attached, and without hello need toodetermine hello true size of data disk.</span></span>


## <a name="mount-hello-attached-data-disk"></a><span data-ttu-id="b4600-152">Hello 연결 된 데이터 디스크를 탑재</span><span class="sxs-lookup"><span data-stu-id="b4600-152">Mount hello attached data disk</span></span>

1. <span data-ttu-id="b4600-153">RDP tooyour hello 적절 한 자격 증명을 사용 하 여 VM의 문제를 해결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-153">RDP tooyour troubleshooting VM using hello appropriate credentials.</span></span> <span data-ttu-id="b4600-154">hello 다음 예제에서는 다운로드 hello 라는 VM에 대 한 RDP 연결 파일 hello `myVMRecovery` 이라는 hello 리소스 그룹에 `myResourceGroup`, 너무 다운로드`C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="b4600-154">hello following example downloads hello RDP connection file for hello VM named `myVMRecovery` in hello resource group named `myResourceGroup`, and downloads it too`C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="b4600-155">hello 데이터 디스크가 자동으로 감지 되 고 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-155">hello data disk is automatically detected and attached.</span></span> <span data-ttu-id="b4600-156">다음과 같이 hello 목록은 연결 된 볼륨이 toodetermine hello 드라이브 문자를 보려면:</span><span class="sxs-lookup"><span data-stu-id="b4600-156">View hello list of attached volumes toodetermine hello drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="b4600-157">다음 예제 출력 hello hello 가상 하드 디스크는 디스크를 연결 표시 **2**합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-157">hello following example output shows hello virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="b4600-158">(사용할 수 있습니다 `Get-Volume` tooview hello 드라이브 문자):</span><span class="sxs-lookup"><span data-stu-id="b4600-158">(You can also use `Get-Volume` tooview hello drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="b4600-159">원래 가상 하드 디스크의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="b4600-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="b4600-160">이제 hello 기존 가상 하드 디스크를 탑재, 모든 유지 관리 및 문제 해결 단계는 필요에 따라 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-160">With hello existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="b4600-161">Hello 문제를 해결 한 후 단계를 수행 하는 hello로 계속 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-161">Once you have addressed hello issues, continue with hello following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="b4600-162">원래 가상 하드 디스크의 탑재 해제 및 분리</span><span class="sxs-lookup"><span data-stu-id="b4600-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="b4600-163">프로그램 오류가 해결 되 면 분리 하 고 문제 해결 VM에서 hello 기존 가상 하드 디스크를 분리 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-163">Once your errors are resolved, you unmount and detach hello existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="b4600-164">VM의 문제를 해결 하는 hello 가상 하드 디스크 toohello 연결 hello 임대가 해제 될 때까지 다른 VM과 가상 하드 디스크를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-164">You cannot use your virtual hard disk with any other VM until hello lease attaching hello virtual hard disk toohello troubleshooting VM is released.</span></span>

1. <span data-ttu-id="b4600-165">RDP 세션에서 복구 VM에 hello 데이터 디스크를 분리 하십시오.</span><span class="sxs-lookup"><span data-stu-id="b4600-165">From within your RDP session, unmount hello data disk on your recovery VM.</span></span> <span data-ttu-id="b4600-166">이전 hello에서 hello 디스크 번호를 필요한 `Get-Disk` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b4600-166">You need hello disk number from hello previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="b4600-167">다음을 사용 하 여 `Set-Disk` 오프 라인으로 tooset hello 디스크:</span><span class="sxs-lookup"><span data-stu-id="b4600-167">Then, use `Set-Disk` tooset hello disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="b4600-168">이제 hello 디스크 사용 하 여 오프 라인으로 설정 확인 `Get-Disk` 다시 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-168">Confirm hello disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="b4600-169">hello 다음 예제 출력과 hello 디스크 이제 오프 라인으로 설정:</span><span class="sxs-lookup"><span data-stu-id="b4600-169">hello following example output shows hello disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="b4600-170">RDP 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-170">Exit your RDP session.</span></span> <span data-ttu-id="b4600-171">Azure PowerShell 세션에서 VM의 문제를 해결 하는 hello에서 hello 가상 하드 디스크를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-171">From your Azure PowerShell session, remove hello virtual hard disk from hello troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="b4600-172">원래 하드 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="b4600-172">Create VM from original hard disk</span></span>
<span data-ttu-id="b4600-173">원래 가상 하드 디스크에서 VM에서 사용할 toocreate [이 Azure 리소스 관리자 템플릿을](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-173">toocreate a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="b4600-174">실제 JSON 템플릿 hello 링크 hello에 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-174">hello actual JSON template is at hello following link:</span></span>

- <span data-ttu-id="b4600-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="b4600-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="b4600-176">hello에서 VHD URL hello를 사용 하 여 기존 가상 네트워크를으로 VM을 배포 하는 hello 템플릿 이전 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-176">hello template deploys a VM into an existing virtual network, using hello VHD URL from hello earlier command.</span></span> <span data-ttu-id="b4600-177">hello 다음 예제에서는 배포 이라는 hello 템플릿 toohello 리소스 그룹 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4600-177">hello following example deploys hello template toohello resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="b4600-178">VM 이름, 운영 체제 유형 및 v M 크기와 같은 hello 서식 파일에 대 한 응답 hello 메시지 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-178">Answer hello prompts for hello template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="b4600-179">hello `osDiskVhdUri` hello 기존 가상 하드 디스크 toohello VM 문제 해결을 연결할 때 이전에 사용 되는 동일한 hello 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-179">hello `osDiskVhdUri` is hello same as previously used when attaching hello existing virtual hard disk toohello troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="b4600-180">부트 진단 다시 사용</span><span class="sxs-lookup"><span data-stu-id="b4600-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="b4600-181">Hello 기존 가상 하드 디스크에서 VM을 만들 때 부트 진단이 자동으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-181">When you create your VM from hello existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="b4600-182">hello 다음 예에서는 가상 컴퓨터 V hello에 진단 확장 hello `myVMDeployed` 이라는 hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="b4600-182">hello following example enables hello diagnostic extension on hello VM named `myVMDeployed` in hello resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="b4600-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b4600-183">Next steps</span></span>
<span data-ttu-id="b4600-184">Tooyour VM을 연결 하는 데 문제가 있는 경우 참조 [문제를 해결 하는 RDP 연결 tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="b4600-184">If you are having issues connecting tooyour VM, see [Troubleshoot RDP connections tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b4600-185">VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Windows VM에서 응용 프로그램 연결 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4600-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="b4600-186">Resource Manager를 사용하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b4600-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
