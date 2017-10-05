---
title: "Azure에서 관리 이미지 만들기 | Microsoft Docs"
description: "Azure에서 일반화된 VM 또는 VHD의 관리 이미지를 만듭니다. 이미지를 사용하여 관리 디스크를 사용하는 여러 VM을 만들 수 있습니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: f64b81489ab426b50ec89af369e1581ac71848be
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="0f4b6-104">Azure에서 일반화된 VM의 관리 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4b6-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="0f4b6-105">저장소 계정에 관리 디스크 또는 비관리 디스크로 저장되는 일반화된 VM으로 관리 이미지 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="0f4b6-106">여러 VM을 만드는 데 이미지를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-106">The image can then be used to create multiple VMs.</span></span> 


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="0f4b6-107">Sysprep을 사용하여 Windows VM 일반화</span><span class="sxs-lookup"><span data-stu-id="0f4b6-107">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="0f4b6-108">Sysprep은 여러 정보 중에서 모든 개인 계정 정보를 제거하고 이미지로 사용할 컴퓨터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-108">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="0f4b6-109">Sysprep에 대한 자세한 내용은 [Sysprep 사용 방법: 소개](http://technet.microsoft.com/library/bb457073.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-109">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="0f4b6-110">가상 컴퓨터에서 실행되는 서버 역할이 Sysprep에서 지원되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-110">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="0f4b6-111">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="0f4b6-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f4b6-112">Azure에 VHD를 업로드하기 전에 Sysprep을 처음으로 실행하는 경우 Sysprep을 실행하기 전에 [VM을 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-112">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="0f4b6-113">Windows 가상 컴퓨터에 로그인</span><span class="sxs-lookup"><span data-stu-id="0f4b6-113">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="0f4b6-114">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-114">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="0f4b6-115">디렉터리를 **%windir%\system32\sysprep**로 변경한 후 `sysprep.exe`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-115">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="0f4b6-116">**시스템 준비 도구** 대화 상자에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화** 확인란을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-116">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="0f4b6-117">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="0f4b6-118">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-118">Click **OK**.</span></span>
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="0f4b6-120">Sysprep이 완료되면 가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-120">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="0f4b6-121">VM을 다시 시작하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-121">Do not restart the VM.</span></span>


## <a name="create-a-managed-image-in-the-portal"></a><span data-ttu-id="0f4b6-122">포털에서 관리 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4b6-122">Create a managed image in the portal</span></span> 

1. <span data-ttu-id="0f4b6-123">[포털](https://portal.azure.com)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-123">Open the [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0f4b6-124">더하기 기호를 클릭하여 새 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-124">Click the plus sign to create a new resource.</span></span>
3. <span data-ttu-id="0f4b6-125">필터 검색에 **이미지**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-125">In the filter search, type **Image**.</span></span>
4. <span data-ttu-id="0f4b6-126">결과에서 **이미지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-126">Select **Image** from the results.</span></span>
5. <span data-ttu-id="0f4b6-127">**이미지** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-127">In the **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="0f4b6-128">**이름**에 이미지 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-128">In **Name**, type a name for the image.</span></span>
7. <span data-ttu-id="0f4b6-129">둘 이상의 구독이 있는 경우 **구독** 드롭다운에서 올바른 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-129">If you have more than one subscription, select the correct one from the **Subscription** drop-down.</span></span>
7. <span data-ttu-id="0f4b6-130">**리소스 그룹**에서 **새로 만들기**를 선택하고 이름을 입력하거나 **기존 항목**을 선택하고 드롭다운 목록에서 사용할 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group to use from the drop-down list.</span></span>
8. <span data-ttu-id="0f4b6-131">**위치**에서 리소스 그룹의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-131">In **Location**, choose the location of your resource group.</span></span>
9. <span data-ttu-id="0f4b6-132">**OS 유형**에서 Windows 또는 Linux 중에 운영 체제 유형을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-132">In **OS type** select the type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="0f4b6-133">**저장소 Blob**에서 **찾아보기**를 클릭하여 Azure Storage에서 VHD를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-133">In **Storage blob**, click **Browse** to look for the VHD in your Azure storage.</span></span>
12. <span data-ttu-id="0f4b6-134">**계정 유형**에서 Standard_LRS 또는 Premium_LRS를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="0f4b6-135">표준은 하드 디스크 드라이브를 사용하고 프리미엄은 반도체 드라이브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="0f4b6-136">둘 다 로컬 중복 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="0f4b6-137">**디스크 캐싱**에서 적절한 디스크 캐싱 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-137">In **Disk caching** select the appropriate disk caching option.</span></span> <span data-ttu-id="0f4b6-138">옵션은 **없음**, **읽기 전용** 및 **읽기/쓰기**입니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-138">The options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="0f4b6-139">선택 사항: **+ 데이터 디스크 추가**를 클릭하여 이미지에 기존 데이터 디스크를 추가할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-139">Optional: You can also add an existing data disk to the image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="0f4b6-140">선택을 마치면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="0f4b6-141">이미지가 생성되면 선택한 리소스 그룹의 리소스 목록에 **이미지** 리소스로 표시될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-141">After the image is created, you will see it as an **Image** resource in the list of resources in the resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="0f4b6-142">Powershell을 사용하여 VM 관리 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4b6-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="0f4b6-143">VM에서 직접 이미지를 만들면 OS 디스크와 데이터 디스크를 포함하여 VM에 연결된 모든 디스크가 이미지에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-143">Creating an image directly from the VM ensures that the image includes all of the disks associated with the VM, including the OS Disk and any data disks.</span></span>


<span data-ttu-id="0f4b6-144">시작하기 전에 AzureRM.Compute PowerShell 모듈이 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-144">Before you begin, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="0f4b6-145">다음 명령을 실행하여 PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-145">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="0f4b6-146">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="0f4b6-147">일부 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="0f4b6-148">VM의 할당이 취소되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-148">Make sure the VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="0f4b6-149">가상 컴퓨터의 상태를 **일반화됨**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-149">Set the status of the virtual machine to **Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="0f4b6-150">가상 컴퓨터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-150">Get the virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="0f4b6-151">이미지 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-151">Create the image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="0f4b6-152">이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-152">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="0f4b6-153">PowerShell에서 VHD 관리 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4b6-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="0f4b6-154">일반화된 OS VHD를 사용하여 관리 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="0f4b6-155">먼저, 공통 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-155">First, set the common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="0f4b6-156">VM을 중지/할당 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-156">Step\deallocate the VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="0f4b6-157">VM을 일반화됨으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-157">Mark the VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="0f4b6-158">일반화된 OS VHD를 사용하여 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-158">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="0f4b6-159">Powershell을 사용하여 스냅숏으로 관리 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4b6-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="0f4b6-160">일반화된 VM에서 VHD 스냅숏으로 관리 이미지를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-160">You can also create a managed image from a snapshot of the VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="0f4b6-161">일부 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="0f4b6-162">스냅숏을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-162">Get the snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="0f4b6-163">이미지 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-163">Create the image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="0f4b6-164">이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-164">Create the image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="0f4b6-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f4b6-165">Next steps</span></span>
- <span data-ttu-id="0f4b6-166">이제 [일반화된 관리 이미지로 VM 만들기](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4b6-166">Now you can [create a VM from the generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>  

