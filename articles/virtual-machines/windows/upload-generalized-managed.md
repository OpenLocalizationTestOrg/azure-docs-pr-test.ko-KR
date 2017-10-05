---
title: "일반화된 온-프레미스 VHD에서 관리되는 Azure VM 만들기 | Microsoft Docs"
description: "일반화된 VHD를 Azure에 업로드하고 이를 사용하여 Resource Manager 배포 모델에서 새 VM을 만듭니다."
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: d802ba16ecb4e32e2adb7be3a8e99c72a1625841
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-to-create-new-vms-in-azure"></a><span data-ttu-id="0f4af-103">일반화된 VHD를 업로드하고 사용하여 Azure에서 새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4af-103">Upload a generalized VHD and use it to create new VMs in Azure</span></span>

<span data-ttu-id="0f4af-104">이 항목에서는 PowerShell을 사용하여 일반화된 VM의 VHD를 Azure에 업로드하고, VHD에서 이미지를 만들고, 해당 이미지에서 새 VM을 만드는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-104">This topic walks you through using PowerShell to upload a VHD of a generalized VM to Azure, create an image from the VHD and create a new VM from that image.</span></span> <span data-ttu-id="0f4af-105">다른 클라우드 또는 온-프레미스 가상화 도구에서 내보낸 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="0f4af-106">새 VM에 대해 [Managed Disks](managed-disks-overview.md)를 사용하면 VM 관리를 간소화하고 VM이 가용성 집합에 배치되는 경우 가용성이 증가됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-106">Using [Managed Disks](managed-disks-overview.md) for the new VM simplifies the VM managment and provides better availability when the VM is placed in an availability set.</span></span> 

<span data-ttu-id="0f4af-107">샘플 스크립트를 사용하려면 [Azure에 VHD를 업로드하고 새 VM을 만드는 샘플 스크립트](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4af-107">If you want to use a sample script, see [Sample script to upload a VHD to Azure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0f4af-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0f4af-108">Before you begin</span></span>

- <span data-ttu-id="0f4af-109">Azure에 VHD를 업로드하기 전에 [Azure에 업로드할 Windows VHD 또는 VHDX 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-109">Before uploading any VHD to Azure, you should follow [Prepare a Windows VHD or VHDX to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="0f4af-110">[Managed Disks](managed-disks-overview.md)로 마이그레이션을 시작하기 전에 [Managed Disks로 마이그레이션하기 위한 계획](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks)을 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4af-110">Review [Plan for the migration to Managed Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration to [Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="0f4af-111">AzureRM.Compute PowerShell 모듈이 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-111">Make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="0f4af-112">다음 명령을 실행하여 PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-112">Run the following command to install it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="0f4af-113">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4af-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-the-windows-vm-using-sysprep"></a><span data-ttu-id="0f4af-114">Sysprep을 사용하여 Windows VM 일반화</span><span class="sxs-lookup"><span data-stu-id="0f4af-114">Generalize the Windows VM using Sysprep</span></span>

<span data-ttu-id="0f4af-115">Sysprep은 여러 정보 중에서 모든 개인 계정 정보를 제거하고 이미지로 사용할 컴퓨터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-115">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="0f4af-116">Sysprep에 대한 자세한 내용은 [Sysprep 사용 방법: 소개](http://technet.microsoft.com/library/bb457073.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4af-116">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="0f4af-117">가상 컴퓨터에서 실행되는 서버 역할이 Sysprep에서 지원되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-117">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="0f4af-118">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="0f4af-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f4af-119">Azure에 VHD를 업로드하기 전에 Sysprep을 처음으로 실행하는 경우 Sysprep을 실행하기 전에 [VM을 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-119">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="0f4af-120">Windows 가상 컴퓨터에 로그인</span><span class="sxs-lookup"><span data-stu-id="0f4af-120">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="0f4af-121">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-121">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="0f4af-122">디렉터리를 **%windir%\system32\sysprep**로 변경한 후 `sysprep.exe`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-122">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="0f4af-123">**시스템 준비 도구** 대화 상자에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화** 확인란을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-123">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="0f4af-124">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="0f4af-125">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-125">Click **OK**.</span></span>
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="0f4af-127">Sysprep이 완료되면 가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-127">When Sysprep completes, it shuts down the virtual machine.</span></span> <span data-ttu-id="0f4af-128">VM을 다시 시작하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-128">Do not restart the VM.</span></span>



## <a name="log-in-to-azure"></a><span data-ttu-id="0f4af-129">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="0f4af-129">Log in to Azure</span></span>
<span data-ttu-id="0f4af-130">PowerShell 버전 1.4 이상을 아직 설치하지 않은 경우 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4af-130">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="0f4af-131">Azure PowerShell을 열고 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-131">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="0f4af-132">Azure 계정 자격 증명을 입력하기 위한 팝업 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-132">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="0f4af-133">사용 가능한 구독에 대한 구독을 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-133">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="0f4af-134">구독 ID를 사용하여 올바른 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-134">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="0f4af-135">*<subscriptionID>*를 올바른 구독의 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-135">Replace *<subscriptionID>* with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-the-storage-account"></a><span data-ttu-id="0f4af-136">저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="0f4af-136">Get the storage account</span></span>
<span data-ttu-id="0f4af-137">업로드한 VM 이미지를 저장할 Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-137">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="0f4af-138">기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="0f4af-139">VHD를 사용하여 VM의 Managed Disk를 만드는 경우 저장소 계정 위치가 VM을 만들 위치와 동일해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-139">If you will be using the VHD to create a managed disk for a VM, the storage account location must be same the location where you will be creating the VM.</span></span>

<span data-ttu-id="0f4af-140">사용 가능한 저장소 계정을 표시하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-140">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="0f4af-141">기존 저장소 계정을 사용하려면 [VM 이미지 업로드](#upload-the-vm-vhd-to-your-storage-account) 섹션을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-141">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="0f4af-142">저장소 계정을 만들어야 하는 경우 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-142">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="0f4af-143">저장소 계정을 만들어야 하는 리소스 그룹의 이름을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-143">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="0f4af-144">구독의 모든 리소스 그룹을 찾으려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-144">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="0f4af-145">**미국 동부** 지역에 **myResourceGroup** 이라는 이름의 리소스 그룹을 만들려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-145">To create a resource group named **myResourceGroup** in the **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="0f4af-146">[New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet을 사용하여 이 리소스 그룹에 **mystorageaccount**라는 이름의 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-146">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="0f4af-147">-SkuName에 대한 유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="0f4af-148">**Standard_LRS** - 로컬 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="0f4af-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="0f4af-149">**Standard_ZRS** - 영역 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="0f4af-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="0f4af-150">**Standard_GRS** - 지역 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="0f4af-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="0f4af-151">**Standard_RAGRS** - 읽기 액세스 지역 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="0f4af-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="0f4af-152">**Premium_LRS** - 프리미엄 로컬 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="0f4af-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="0f4af-153">저장소 계정에 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="0f4af-153">Upload the VHD to your storage account</span></span>

<span data-ttu-id="0f4af-154">[Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet을 사용하여 저장소 계정의 컨테이너에 VHD를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-154">Use the [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet to upload the VHD to a container in your storage account.</span></span> <span data-ttu-id="0f4af-155">이 예제에서는 *"C:\Users\Public\Documents\Virtual hard disks\"*에서 *myResourceGroup* 리소스 그룹의 *mystorageaccount*라는 저장소 계정에 파일 *myVHD.vhd*를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-155">This example uploads the file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* to a storage account named *mystorageaccount* in the *myResourceGroup* resource group.</span></span> <span data-ttu-id="0f4af-156">파일은 *mycontainer*라는 컨테이너에 배치되고 새 파일 이름은 *myUploadedVHD.vhd*가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-156">The file will be placed into the container named *mycontainer* and the new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="0f4af-157">성공하면 다음과 유사한 응답을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-157">If successful, you get a response that looks similar to this:</span></span>

```powershell
MD5 hash is being calculated for the file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for the operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="0f4af-158">이 명령은 네트워크 연결 및 VHD 파일의 크기에 따라 완료하는 데 다소 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-158">Depending on your network connection and the size of your VHD file, this command may take a while to complete</span></span>

<span data-ttu-id="0f4af-159">업로드된 VHD를 사용하여 Managed Disk 또는 새 VM을 만들려면 나중에 사용할 수 있도록 **대상 URI** 경로를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-159">Save the **Destination URI** path to use later if you are going to create a managed disk or a new VM using the uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="0f4af-160">VHD를 업로드하기 위한 기타 옵션</span><span class="sxs-lookup"><span data-stu-id="0f4af-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="0f4af-161">또한 다음 방법 중 하나를 사용하여 저장소 계정에 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-161">You can also upload a VHD to your storage account using one of the following:</span></span>

- [<span data-ttu-id="0f4af-162">AZCopy</span><span class="sxs-lookup"><span data-stu-id="0f4af-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="0f4af-163">Azure 저장소 Blob 복사 API</span><span class="sxs-lookup"><span data-stu-id="0f4af-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="0f4af-164">Azure Storage 탐색기 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="0f4af-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="0f4af-165">저장소 가져오기/내보내기 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="0f4af-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="0f4af-166">예상 업로드 시간이 7일보다 긴 경우 가져오기/내보내기 서비스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="0f4af-167">[DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html)를 사용하여 데이터 크기 및 전송 단위로 시간을 예측할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) to estimate the time from data size and transfer unit.</span></span> 
    <span data-ttu-id="0f4af-168">가져오기/내보내기를 사용하여 표준 저장소 계정을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-168">Import/Export can be used to copy to a standard storage account.</span></span> <span data-ttu-id="0f4af-169">AzCopy와 같은 도구를 사용하여 표준 저장소에서 프리미엄 저장소 계정으로 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-169">You will need to copy from standard storage to premium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-the-uploaded-vhd"></a><span data-ttu-id="0f4af-170">업로드된 VHD에서 관리되는 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4af-170">Create a managed image from the uploaded VHD</span></span> 

<span data-ttu-id="0f4af-171">일반화된 OS VHD를 사용하여 관리 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="0f4af-172">사용자 고유의 정보로 값을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-172">Replace the values with your own information.</span></span>


1.  <span data-ttu-id="0f4af-173">먼저, 공통 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-173">First, set the common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="0f4af-174">일반화된 OS VHD를 사용하여 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-174">Create the image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="0f4af-175">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4af-175">Create a virtual network</span></span>
<span data-ttu-id="0f4af-176">[가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 vNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-176">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="0f4af-177">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-177">Create the subnet.</span></span> <span data-ttu-id="0f4af-178">이 예제에서는 주소 접두사로 *10.0.0.0/24*를 사용하는 *mySubnet*이라는 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-178">This example creates a subnet named *mySubnet* with the address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="0f4af-179">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4af-179">Create the virtual network.</span></span> <span data-ttu-id="0f4af-180">이 예제에서는 주소 접두사로 *10.0.0.0/16*을 사용하는 *myVnet*이라는 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-180">This example creates a virtual network named *myVnet* with the address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="0f4af-181">공용 IP 주소 및 네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4af-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="0f4af-182">가상 네트워크에서 가상 컴퓨터와 통신하려면 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-182">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="0f4af-183">공용 IP 주소 만들기.</span><span class="sxs-lookup"><span data-stu-id="0f4af-183">Create a public IP address.</span></span> <span data-ttu-id="0f4af-184">이 예에서는 *myPip*라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="0f4af-185">NIC 만들기.</span><span class="sxs-lookup"><span data-stu-id="0f4af-185">Create the NIC.</span></span> <span data-ttu-id="0f4af-186">이 예에서는 **myNic**라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="0f4af-187">네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4af-187">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="0f4af-188">RDP를 사용하여 VM에 로그인할 수 있으려면 포트 3389에 대한 RDP 액세스를 허용하는 NSG(네트워크 보안 규칙)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-188">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="0f4af-189">이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 *myRdpRule*이라는 규칙을 포함하는 *myNsg*로 명명된 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="0f4af-190">NSG에 대한 자세한 내용은 [PowerShell을 사용하여 Azure에서 VM으로 포트 열기](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4af-190">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="0f4af-191">가상 네트워크에 대한 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4af-191">Create a variable for the virtual network</span></span>

<span data-ttu-id="0f4af-192">완료된 가상 네트워크에 대한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-192">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="0f4af-193">VM에 대한 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="0f4af-193">Get the credentials for the VM</span></span>

<span data-ttu-id="0f4af-194">다음 cmdlet을 사용하면 VM에 원격으로 액세스하기 위해 로컬 관리자 계정으로 사용할 새 사용자 이름 및 암호를 입력할 수 있는 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-194">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-the-vm-name-and-size-to-the-vm-configuration"></a><span data-ttu-id="0f4af-195">VM 구성에 VM의 이름과 크기를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-195">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="0f4af-196">새 VM에 대한 원본 이미지로 VM 이미지 설정</span><span class="sxs-lookup"><span data-stu-id="0f4af-196">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="0f4af-197">관리되는 VM 이미지의 ID를 사용하여 원본 이미지를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-197">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="0f4af-198">OS 구성을 설정하고 NIC를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-198">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="0f4af-199">저장소 유형(PremiumLRS 또는 StandardLRS) 및 OS 디스크의 크기를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-199">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="0f4af-200">이 예제에서는 계정 유형을 *PremiumLRS*로, 디스크 크기를 *128GB*로, 디스크 캐싱을 *ReadWrite*로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-200">This example sets the account type to *PremiumLRS*, the disk size to *128 GB* and disk caching to *ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="0f4af-201">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0f4af-201">Create the VM</span></span>

<span data-ttu-id="0f4af-202">**$vm** 변수에 저장한 구성을 사용하여 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-202">Create the new VM using the configuration stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="0f4af-203">VM이 만들어졌는지 확인</span><span class="sxs-lookup"><span data-stu-id="0f4af-203">Verify that the VM was created</span></span>
<span data-ttu-id="0f4af-204">완료되면 새로 만든 VM은 [Azure 포털](https://portal.azure.com)에서 **찾아보기** > **가상 컴퓨터**에 표시되며 다음 PowerShell 명령을 사용해도 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-204">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="0f4af-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0f4af-205">Next steps</span></span>

<span data-ttu-id="0f4af-206">새 가상 컴퓨터에 로그인하려면 [포털](https://portal.azure.com)에서 VM으로 이동한 다음 **연결**을 클릭하고 원격 데스크톱 RDP 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-206">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="0f4af-207">원본 가상 컴퓨터의 계정 자격 증명을 사용하여 새 가상 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0f4af-207">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="0f4af-208">자세한 내용은 [Windows를 실행하는 Azure 가상 컴퓨터에 연결하고 로그온하는 방법](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0f4af-208">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

