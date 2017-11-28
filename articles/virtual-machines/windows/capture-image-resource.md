---
title: "Azure에서 관리 되는 이미지 aaaCreate | Microsoft Docs"
description: "Azure에서 일반화된 VM 또는 VHD의 관리 이미지를 만듭니다. 이미지 toocreate 사용 되는 관리 되는 디스크를 사용 하는 여러 Vm 수 있습니다."
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
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a><span data-ttu-id="1aa20-104">Azure에서 일반화된 VM의 관리 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="1aa20-104">Create a managed image of a generalized VM in Azure</span></span>

<span data-ttu-id="1aa20-105">저장소 계정에 관리 디스크 또는 비관리 디스크로 저장되는 일반화된 VM으로 관리 이미지 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-105">A managed image resource can be created from a generalized VM that is stored as either a managed disk or an unmanaged disk in a storage account.</span></span> <span data-ttu-id="1aa20-106">이미지 수를 hello 다음 toocreate 사용 되는 여러 Vm 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-106">hello image can then be used toocreate multiple VMs.</span></span> 


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="1aa20-107">일반화 hello Sysprep를 사용 하 여 Windows VM</span><span class="sxs-lookup"><span data-stu-id="1aa20-107">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="1aa20-108">Sysprep는 특히, 모든 개인 계정 정보를 제거 하 고 이미지 형식으로 사용 되는 hello 컴퓨터 toobe를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-108">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="1aa20-109">Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-109">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="1aa20-110">Hello 컴퓨터에서 실행 되는 hello 서버 역할과 Sysprep에서 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-110">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="1aa20-111">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="1aa20-111">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1aa20-112">를 사용 하 여 VHD tooAzure hello에 대 한 처음으로 업로드 하기 전에 Sysprep를 실행 하는 경우 했는지 확인 [VM 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep를 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="1aa20-112">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="1aa20-113">Windows 가상 컴퓨터 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-113">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="1aa20-114">Hello 명령 프롬프트 창을 관리자 권한으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-114">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="1aa20-115">Hello 디렉터리도 변경**%windir%\system32\sysprep**, 한 다음 실행 `sysprep.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-115">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="1aa20-116">Hello에 **시스템 준비 도구** 대화 상자에서 **입력 시스템을 기본 OOBE (Experience)**, 해당 hello 있는지 확인 하 고 **일반화** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-116">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="1aa20-117">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-117">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="1aa20-118">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-118">Click **OK**.</span></span>
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="1aa20-120">Sysprep이 완료 된 hello 가상 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-120">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="1aa20-121">Hello VM을 다시 시작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-121">Do not restart hello VM.</span></span>


## <a name="create-a-managed-image-in-hello-portal"></a><span data-ttu-id="1aa20-122">Hello 포털에서 관리 되는 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="1aa20-122">Create a managed image in hello portal</span></span> 

1. <span data-ttu-id="1aa20-123">열기 hello [포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-123">Open hello [portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1aa20-124">클릭 하 여 새 리소스를 더하기 기호 toocreate hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-124">Click hello plus sign toocreate a new resource.</span></span>
3. <span data-ttu-id="1aa20-125">Hello 필터 검색 입력 **이미지**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-125">In hello filter search, type **Image**.</span></span>
4. <span data-ttu-id="1aa20-126">선택 **이미지** hello 결과에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-126">Select **Image** from hello results.</span></span>
5. <span data-ttu-id="1aa20-127">Hello에 **이미지** 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-127">In hello **Image** blade, click **Create**.</span></span>
6. <span data-ttu-id="1aa20-128">**이름**를 hello 이미지에 대 한 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-128">In **Name**, type a name for hello image.</span></span>
7. <span data-ttu-id="1aa20-129">선택 hello hello에서 올바른 이름이 둘 이상의 구독이 있으면 **구독** 드롭 다운 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-129">If you have more than one subscription, select hello correct one from hello **Subscription** drop-down.</span></span>
7. <span data-ttu-id="1aa20-130">**리소스 그룹** 선택 하거나 **새로 만들기** 이름을 입력 하거나 선택 하 고 **기존 계획에서** 리소스 그룹 toouse hello 드롭 다운 목록에서 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-130">In **Resource Group** either select **Create new** and type in a name, or select **From existing** and select a resource group toouse from hello drop-down list.</span></span>
8. <span data-ttu-id="1aa20-131">**위치**, 리소스 그룹의 hello 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-131">In **Location**, choose hello location of your resource group.</span></span>
9. <span data-ttu-id="1aa20-132">**OS 유형이** hello 유형의 Windows 또는 Linux 운영 체제를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-132">In **OS type** select hello type of operating system, either Windows or Linux.</span></span>
11. <span data-ttu-id="1aa20-133">**저장소 blob**, 클릭 **찾아보기** toolook Azure 저장소에 VHD hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-133">In **Storage blob**, click **Browse** toolook for hello VHD in your Azure storage.</span></span>
12. <span data-ttu-id="1aa20-134">**계정 유형**에서 Standard_LRS 또는 Premium_LRS를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-134">In **Account type** choose Standard_LRS or Premium_LRS.</span></span> <span data-ttu-id="1aa20-135">표준은 하드 디스크 드라이브를 사용하고 프리미엄은 반도체 드라이브를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-135">Standard uses hard-disk drives and Premium uses solid-state drives.</span></span> <span data-ttu-id="1aa20-136">둘 다 로컬 중복 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-136">Both use locally-redundant storage.</span></span>
13. <span data-ttu-id="1aa20-137">**디스크 캐싱** 선택 hello 적합 한 디스크 캐싱 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-137">In **Disk caching** select hello appropriate disk caching option.</span></span> <span data-ttu-id="1aa20-138">hello 옵션은 **None**, **읽기 전용** 및 **읽기/쓰기**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-138">hello options are **None**, **Read-only** and **Read\write**.</span></span>
14. <span data-ttu-id="1aa20-139">선택 사항: 추가할 수 있습니다도 기존 데이터 디스크 toohello 이미지를 클릭 하 여 **+ 추가 데이터 디스크**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-139">Optional: You can also add an existing data disk toohello image by clicking **+ Add data disk**.</span></span>  
15. <span data-ttu-id="1aa20-140">선택을 마치면 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-140">When you are done making your selections, click **Create**.</span></span>
16. <span data-ttu-id="1aa20-141">Hello 이미지를 만든 후 나타납니다로 **이미지** hello 선택한 hello 리소스 그룹의 리소스 목록에는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-141">After hello image is created, you will see it as an **Image** resource in hello list of resources in hello resource group you chose.</span></span>



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a><span data-ttu-id="1aa20-142">Powershell을 사용하여 VM 관리 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="1aa20-142">Create a managed image of a VM using Powershell</span></span>

<span data-ttu-id="1aa20-143">VM hello 이미지를 사용 하면 hello에서 직접 이미지를 만들기 hello hello OS 디스크 및 데이터 디스크를 포함 하 여 VM과 연결 된 hello 디스크를 모두 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-143">Creating an image directly from hello VM ensures that hello image includes all of hello disks associated with hello VM, including hello OS Disk and any data disks.</span></span>


<span data-ttu-id="1aa20-144">시작 하기 전에 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-144">Before you begin, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="1aa20-145">실행 명령 tooinstall 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-145">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="1aa20-146">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1aa20-146">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


1. <span data-ttu-id="1aa20-147">일부 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-147">Create some variables.</span></span>

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. <span data-ttu-id="1aa20-148">VM 할당 취소 되어 있는지 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-148">Make sure hello VM has been deallocated.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="1aa20-149">Hello 가상 컴퓨터의 hello 상태를 너무 설정**일반화 됨으로**합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-149">Set hello status of hello virtual machine too**Generalized**.</span></span> 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. <span data-ttu-id="1aa20-150">Hello 가상 컴퓨터를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-150">Get hello virtual machine.</span></span> 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. <span data-ttu-id="1aa20-151">Hello 이미지 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-151">Create hello image configuration.</span></span>

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. <span data-ttu-id="1aa20-152">Hello 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-152">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a><span data-ttu-id="1aa20-153">PowerShell에서 VHD 관리 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="1aa20-153">Create a managed image of a VHD in PowerShell</span></span>

<span data-ttu-id="1aa20-154">일반화된 OS VHD를 사용하여 관리 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-154">Create a managed image using your generalized OS VHD.</span></span>


1.  <span data-ttu-id="1aa20-155">먼저, hello 공통 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-155">First, set hello common parameters:</span></span>

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. <span data-ttu-id="1aa20-156">Step\deallocate hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-156">Step\deallocate hello VM.</span></span>

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. <span data-ttu-id="1aa20-157">Hello 일반화 된 것과 같이 VM을 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-157">Mark hello VM as generalized.</span></span>

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  <span data-ttu-id="1aa20-158">일반화 된 운영 체제 VHD를 사용 하 여 hello 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-158">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a><span data-ttu-id="1aa20-159">Powershell을 사용하여 스냅숏으로 관리 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="1aa20-159">Create a managed image from a snapshot using Powershell</span></span>

<span data-ttu-id="1aa20-160">Hello 일반화 된 VM에서 VHD의 스냅샷을에서 관리 되는 이미지를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-160">You can also create a managed image from a snapshot of hello VHD from a generalized VM.</span></span>

    
1. <span data-ttu-id="1aa20-161">일부 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-161">Create some variables.</span></span> 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. <span data-ttu-id="1aa20-162">Hello 스냅숏을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-162">Get hello snapshot.</span></span>

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. <span data-ttu-id="1aa20-163">Hello 이미지 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-163">Create hello image configuration.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. <span data-ttu-id="1aa20-164">Hello 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-164">Create hello image.</span></span>

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a><span data-ttu-id="1aa20-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1aa20-165">Next steps</span></span>
- <span data-ttu-id="1aa20-166">이제 [일반화 hello 관리 되는 이미지에서 VM을 만들](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1aa20-166">Now you can [create a VM from hello generalized managed image](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>    

