---
title: "Azure PowerShell에서 Windows 문제 해결 VM 사용 | Microsoft Docs"
description: "Azure PowerShell을 사용하여 OS 디스크를 복구 VM에 연결함으로써 Azure에서 Windows VM 문제를 해결하는 방법을 알아봅니다."
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
ms.openlocfilehash: 8b7821b4285e73d461af426bfdfb3fdcc4454517
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-azure-powershell"></a><span data-ttu-id="7de4e-103">Azure PowerShell을 사용하여 OS 디스크를 복구 VM에 연결함으로써 Windows VM 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7de4e-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="7de4e-104">Azure에서 Windows VM(가상 컴퓨터)에 부팅 또는 디스크 오류가 발생하는 경우 가상 하드 디스크에서 바로 문제 해결 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="7de4e-105">일반적인 예로는 응용 프로그램 업데이트가 실패하여 VM이 성공적으로 부팅되지 않는 경우입니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="7de4e-106">이 문서에는 가상 하드 디스크를 다른 Windows VM에 연결하여 모든 오류를 수정한 후 원래 VM을 다시 만들기 위해 Azure PowerShell을 사용하는 방법을 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-106">This article details how to use Azure PowerShell to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="7de4e-107">복구 프로세스 개요</span><span class="sxs-lookup"><span data-stu-id="7de4e-107">Recovery process overview</span></span>
<span data-ttu-id="7de4e-108">문제 해결 프로세스는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="7de4e-109">문제가 발생하는 VM을 삭제하여, 가상 하드 디스크를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="7de4e-110">문제 해결을 위해 가상 하드 디스크를 다른 Windows VM에 연결하고 탑재합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="7de4e-111">문제 해결 VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="7de4e-112">파일을 편집하거나 도구를 실행하여 원래의 가상 하드 디스크에서 문제를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="7de4e-113">문제 해결 VM에서 가상 하드 디스크를 탑재 해제하고 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="7de4e-114">원래 가상 하드 디스크를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-114">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="7de4e-115">먼저 [최신 Azure PowerShell](/powershell/azure/overview)을 설치하고 구독에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-115">Make sure that you have [the latest Azure PowerShell](/powershell/azure/overview) installed and logged in to your subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="7de4e-116">다음 예제에서 매개 변수 이름을 고유한 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-116">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="7de4e-117">예제 매개 변수 이름에 `myResourceGroup`, `mystorageaccount` 및 `myVM`이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="7de4e-118">부팅 문제 확인</span><span class="sxs-lookup"><span data-stu-id="7de4e-118">Determine boot issues</span></span>
<span data-ttu-id="7de4e-119">Azure에서 VM의 스크린샷을 보고 부팅 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-119">You can view a screenshot of your VM in Azure to help troubleshoot boot issues.</span></span> <span data-ttu-id="7de4e-120">이 스크린샷은 VM이 부팅되지 않는 이유를 확인하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-120">This screenshot can help identify why a VM fails to boot.</span></span> <span data-ttu-id="7de4e-121">다음 예제에서는 리소스 그룹 `myResourceGroup`의 Windows VM `myVM`에서 스크린샷을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-121">The following example gets the screenshot from the Windows VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="7de4e-122">스크린샷을 검토하여 VM이 부팅되지 않는 원인을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-122">Review the screenshot to determine why the VM is failing to boot.</span></span> <span data-ttu-id="7de4e-123">제공된 특정 오류 메시지 또는 오류 코드를 기록해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="7de4e-124">기존 가상 하드 디스크 세부 정보 보기</span><span class="sxs-lookup"><span data-stu-id="7de4e-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="7de4e-125">가상 하드 디스크를 다른 VM에 연결하기 전에 가상 하드 디스크(VHD)의 이름을 식별해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span>

<span data-ttu-id="7de4e-126">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVM`에 대한 정보를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-126">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="7de4e-127">이전 명령의 출력에서 ​​`StorageProfile` 섹션 내의 `Vhd URI`를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-127">Look for `Vhd URI` within the `StorageProfile` section from the output of the preceding command.</span></span> <span data-ttu-id="7de4e-128">다음 잘린 출력 예에서 코드 블록의 끝을 향한 `Vhd URI`를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-128">The following truncated example output shows the `Vhd URI` towards the end of the code block:</span></span>

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


## <a name="delete-existing-vm"></a><span data-ttu-id="7de4e-129">기존 VM 삭제</span><span class="sxs-lookup"><span data-stu-id="7de4e-129">Delete existing VM</span></span>
<span data-ttu-id="7de4e-130">가상 하드 디스크와 VM은 Azure의 두 가지 별개의 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="7de4e-131">가상 하드 디스크에는 운영 체제 자체, 응용 프로그램 및 구성이 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-131">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="7de4e-132">VM 자체는 크기 또는 위치를 정의하고 가상 하드 디스크 또는 가상 네트워크 인터페이스 카드(NIC)와 같은 리소스를 참조하는 메타데이터일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-132">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="7de4e-133">각 가상 하드 디스크에는 VM에 연결할 때 할당된 임대가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-133">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="7de4e-134">VM을 실행하는 동안에도 데이터 디스크를 연결하고 분리할 수 있지만, VM 리소스를 삭제하지 않는 한 OS 디스크를 분리할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-134">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="7de4e-135">해당 VM이 중지 및 할당 취소된 상태에 있을 때에도 임대는 OS 디스크와 VM을 계속 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-135">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="7de4e-136">VM을 복구하는 첫 번째 단계는 자체 VM 리소스를 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-136">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="7de4e-137">VM을 삭제하면 가상 하드 디스크는 저장소 계정에 남게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-137">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="7de4e-138">VM을 삭제한 후 가상 하드 디스크를 다른 VM에 연결하여 문제와 오류를 해결합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-138">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="7de4e-139">다음 예제에서는 리소스 그룹 `myResourceGroup`에서 VM `myVM`을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-139">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="7de4e-140">가상 하드 디스크를 다른 VM에 연결 하기 전에 VM이 삭제 작업을 끝낼 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-140">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="7de4e-141">VM과 연결하는 가상 하드 디스크의 임대는 가상 하드 디스크를 다른 VM에 연결하기 전에 해제해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-141">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="7de4e-142">기존 가상 하드 디스크를 다른 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="7de4e-142">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="7de4e-143">다음 몇 단계에서는 문제 해결을 위해 다른 VM을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-143">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="7de4e-144">기존 가상 하드 디스크를 이 문제 해결 VM에 연결하여 디스크의 콘텐츠를 찾아 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-144">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="7de4e-145">예를 들어 이 프로세스를 사용하면 구성 오류를 수정하거나 추가 응용 프로그램 또는 시스템 로그 파일을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-145">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="7de4e-146">다른 VM을 선택하거나 만들어 문제 해결에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-146">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="7de4e-147">기존 가상 하드 디스크를 연결하는 경우 이전 `Get-AzureRmVM` 명령에서 획득한 디스크에 URL을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-147">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="7de4e-148">다음 예제에서는 리소스 그룹 `myResourceGroup`의 문제 해결 VM `myVMRecovery`에 기존 가상 하드 디스크를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-148">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="7de4e-149">디스크를 추가하려면 디스크의 크기를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-149">Adding a disk requires you to specify the size of the disk.</span></span> <span data-ttu-id="7de4e-150">기존 디스크를 연결할 때 `-DiskSizeInGB`가 `$null`로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-150">As we attach an existing disk, the `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="7de4e-151">이 값은 데이터 디스크의 실제 크기를 확인하지 않아도 데이터 디스크가 올바르게 연결되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-151">This value ensures the data disk is correctly attached, and without the need to determine the true size of data disk.</span></span>


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="7de4e-152">연결된 데이터 디스크 탑재</span><span class="sxs-lookup"><span data-stu-id="7de4e-152">Mount the attached data disk</span></span>

1. <span data-ttu-id="7de4e-153">적절한 자격 증명을 사용하여 문제 해결 VM에 대한 RDP입니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-153">RDP to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="7de4e-154">다음 예에서는 `myResourceGroup`이라는 리소스 그룹에서 `myVMRecovery`라는 VM에 대한 RDP 연결 파일을 `C:\Users\ops\Documents`에 다운로드합니다</span><span class="sxs-lookup"><span data-stu-id="7de4e-154">The following example downloads the RDP connection file for the VM named `myVMRecovery` in the resource group named `myResourceGroup`, and downloads it to `C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="7de4e-155">데이터 디스크가 자동으로 감지되고 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-155">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="7de4e-156">다음과 같이 연결된 볼륨 목록을 보고 드라이브 문자를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-156">View the list of attached volumes to determine the drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="7de4e-157">다음 출력 예에서는 디스크 **2**에 연결된 가상 하드 디스크를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-157">The following example output shows the virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="7de4e-158">(`Get-Volume`을 사용하여 드라이브 문자를 볼 수도 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="7de4e-158">(You can also use `Get-Volume` to view the drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="7de4e-159">원래 가상 하드 디스크의 문제 해결</span><span class="sxs-lookup"><span data-stu-id="7de4e-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="7de4e-160">기존 가상 하드 디스크가 탑재되면 이제 필요에 따라 모든 유지 관리 및 문제 해결 단계를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-160">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="7de4e-161">문제가 해결되면 다음 단계를 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-161">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="7de4e-162">원래 가상 하드 디스크의 탑재 해제 및 분리</span><span class="sxs-lookup"><span data-stu-id="7de4e-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="7de4e-163">오류가 해결되면 문제 해결 VM에서 기존 가상 하드 디스크를 탑재 해제하고 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-163">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="7de4e-164">가상 하드 디스크를 문제 해결 VM에 연결하는 임대가 해제될 때까지 가상 하드 디스크를 다른 VM과 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-164">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="7de4e-165">RDP 세션의 복구 VM에서 데이터 디스크를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-165">From within your RDP session, unmount the data disk on your recovery VM.</span></span> <span data-ttu-id="7de4e-166">이전 `Get-Disk` cmdlet의 디스크 번호가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-166">You need the disk number from the previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="7de4e-167">그런 다음 `Set-Disk`를 사용하여 디스크를 오프라인으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-167">Then, use `Set-Disk` to set the disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="7de4e-168">이제 `Get-Disk`를 다시 사용하여 디스크가 오프라인으로 설정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-168">Confirm the disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="7de4e-169">다음 출력 예에서는 디스크가 오프라인으로 설정되었다는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-169">The following example output shows the disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="7de4e-170">RDP 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-170">Exit your RDP session.</span></span> <span data-ttu-id="7de4e-171">Azure PowerShell 세션의 문제 해결 VM에서 가상 하드 디스크를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-171">From your Azure PowerShell session, remove the virtual hard disk from the troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="7de4e-172">원래 하드 디스크에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="7de4e-172">Create VM from original hard disk</span></span>
<span data-ttu-id="7de4e-173">원래 가상 하드 디스크에서 VM을 만들려면 [이 Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-173">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="7de4e-174">실제 JSON 템플릿은 다음 링크에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-174">The actual JSON template is at the following link:</span></span>

- <span data-ttu-id="7de4e-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span><span class="sxs-lookup"><span data-stu-id="7de4e-175">https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json</span></span>

<span data-ttu-id="7de4e-176">템플릿은 이전 명령의 VHD URL을 사용하여 VM을 기존 가상 네트워크에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-176">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="7de4e-177">다음 예제에서는 리소스 그룹 `myResourceGroup`에 템플릿을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-177">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="7de4e-178">VM 이름, OS 유형 및 VM 크기 등 템플릿에 대한 프롬프트에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-178">Answer the prompts for the template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="7de4e-179">`osDiskVhdUri`는 기존 가상 하드 디스크를 문제 해결 VM에 연결할 때 이전에 사용된 것과 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-179">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="7de4e-180">부트 진단 다시 사용</span><span class="sxs-lookup"><span data-stu-id="7de4e-180">Re-enable boot diagnostics</span></span>

<span data-ttu-id="7de4e-181">기존 가상 하드 디스크에서 VM을 만든 경우 부팅 진단을 자동으로 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-181">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="7de4e-182">다음 예제에서는 리소스 그룹 `myResourceGroup`의 VM `myVMDeployed`에서 진단 확장을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7de4e-182">The following example enables the diagnostic extension on the VM named `myVMDeployed` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="7de4e-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7de4e-183">Next steps</span></span>
<span data-ttu-id="7de4e-184">VM에 연결하는 데 문제가 있는 경우 [Azure VM에 RDP 연결 문제 해결](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7de4e-184">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="7de4e-185">VM에서 실행 중인 응용 프로그램에 액세스하는 데 문제가 있는 경우 [Windows VM에서 응용 프로그램 연결 문제 해결](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7de4e-185">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="7de4e-186">Resource Manager를 사용하는 방법에 대한 자세한 내용은 [Azure Resource Manager 개요](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7de4e-186">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
