---
title: "Azure에서 특수한 디스크로 VM 만들기 | Microsoft Docs"
description: "Resource Manager 배포 모델에서 특수한 비관리 디스크를 연결하여 새 VM을 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 974d89aa96cba94fedfd1acbaf4f1d30ac8e6257
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="d299a-103">저장소 계정의 특수한 VHD에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d299a-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="d299a-104">Powershell을 사용하여 특수한 비관리 디스크를 OS 디스크로 연결하여 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-104">Create a new VM by attaching a specialized unmanaged disk as the OS disk using Powershell.</span></span> <span data-ttu-id="d299a-105">특수한 디스크는 기존 VM의 VHD 복사본으로 사용자 계정, 응용 프로그램 및 원본 VM의 기타 상태 데이터를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-105">A specialized disk is a copy of VHD from an existing VM that maintains the user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="d299a-106">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-106">You have two options:</span></span>
* [<span data-ttu-id="d299a-107">VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="d299a-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="d299a-108">기존 Azure VM의 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="d299a-108">Copy the VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="d299a-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d299a-109">Before you begin</span></span>
<span data-ttu-id="d299a-110">PowerShell을 사용하는 경우 AzureRM.Compute PowerShell 모듈이 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-110">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="d299a-111">다음 명령을 실행하여 PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-111">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="d299a-112">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d299a-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="d299a-113">옵션 1: 특수한 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="d299a-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="d299a-114">Hyper-V와 같은 온-프레미스 가상화 도구를 사용하여 만든 특수한 VM 또는 다른 클라우드에서 내보낸 VM에서 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-114">You can upload the VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-the-vm"></a><span data-ttu-id="d299a-115">VM 준비</span><span class="sxs-lookup"><span data-stu-id="d299a-115">Prepare the VM</span></span>
<span data-ttu-id="d299a-116">온-프레미스 VM을 사용하여 만든 특수한 VHD 또는 다른 클라우드에서 내보낸 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="d299a-117">특수한 VHD는 사용자 계정, 응용 프로그램 및 원본 VM의 다른 상태 데이터를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-117">A specialized VHD maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="d299a-118">새 VM을 만드는데 VHD를 그대로 사용하려는 경우 다음 단계가 완료되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-118">If you intend to use the VHD as-is to create a new VM, ensure the following steps are completed.</span></span> 
  
  * <span data-ttu-id="d299a-119">[Azure에 업로드할 Windows VHD를 준비합니다](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d299a-119">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d299a-120">Sysprep을 사용하여 VM을 일반화하지 **마십시오**.</span><span class="sxs-lookup"><span data-stu-id="d299a-120">**Do not** generalize the VM using Sysprep.</span></span>
  * <span data-ttu-id="d299a-121">모든 게스트 가상화 도구 및 VM에 설치된 에이전트를 제거합니다(예: VMware 도구).</span><span class="sxs-lookup"><span data-stu-id="d299a-121">Remove any guest virtualization tools and agents that are installed on the VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="d299a-122">VM이 DHCP를 통해 해당 IP 주소 및 DNS 설정을 가져오도록 구성되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-122">Ensure the VM is configured to pull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="d299a-123">이렇게 하면 서버를 시작할 때 VNet 내의 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-123">This ensures that the server obtains an IP address within the VNet when it starts up.</span></span> 


### <a name="get-the-storage-account"></a><span data-ttu-id="d299a-124">저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="d299a-124">Get the storage account</span></span>
<span data-ttu-id="d299a-125">업로드한 VM 이미지를 저장할 Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-125">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="d299a-126">기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="d299a-127">사용 가능한 저장소 계정을 표시하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-127">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="d299a-128">기존 저장소 계정을 사용하려면 [VM 이미지 업로드](#upload-the-vm-vhd-to-your-storage-account) 섹션을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-128">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="d299a-129">저장소 계정을 만들어야 하는 경우 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-129">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="d299a-130">저장소 계정을 만들어야 하는 리소스 그룹의 이름을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-130">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="d299a-131">구독의 모든 리소스 그룹을 찾으려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-131">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="d299a-132">**미국 서부** 지역에 **myResourceGroup** 이라는 이름의 리소스 그룹을 만들려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-132">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="d299a-133">[New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet을 사용하여 이 리소스 그룹에 **mystorageaccount**라는 이름의 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-133">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-the-vhd-to-your-storage-account"></a><span data-ttu-id="d299a-134">저장소 계정에 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="d299a-134">Upload the VHD to your storage account</span></span>
<span data-ttu-id="d299a-135">[Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet을 사용하여 저장소 계정의 컨테이너에 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-135">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="d299a-136">이 예제에서는 `"C:\Users\Public\Documents\Virtual hard disks\"`에서 **myResourceGroup** 리소스 그룹의 **mystorageaccount**라는 저장소 계정에 파일 **myVHD.vhd**를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-136">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="d299a-137">파일은 **mycontainer**라는 컨테이너에 배치되고 새 파일 이름은 **myUploadedVHD.vhd**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-137">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="d299a-138">성공하면 다음과 유사한 응답을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-138">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="d299a-139">이 명령은 네트워크 연결 및 VHD 파일의 크기에 따라 완료하는 데 다소 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-139">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="option-2-copy-the-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="d299a-140">옵션 2: 기존 Azure VM에서 VHD 복사</span><span class="sxs-lookup"><span data-stu-id="d299a-140">Option 2: Copy the VHD from an existing Azure VM</span></span>

<span data-ttu-id="d299a-141">중복된 새 VM을 만들 때 사용할 다른 저장소 계정에 VHD를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-141">You can copy a VHD to another storage account to use when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="d299a-142">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="d299a-142">Before you begin</span></span>
<span data-ttu-id="d299a-143">다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-143">Make sure that you:</span></span>

* <span data-ttu-id="d299a-144">**원본 및 대상 저장소 계정**에 대한 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-144">Have information about the **source and destination storage accounts**.</span></span> <span data-ttu-id="d299a-145">원본 VM의 경우 저장소 계정 및 컨테이너 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-145">For the source VM, you need to have the storage account and container names.</span></span> <span data-ttu-id="d299a-146">일반적으로 컨테이너 이름은 **vhds**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-146">Usually, the container name will be **vhds**.</span></span> <span data-ttu-id="d299a-147">또한 대상 저장소 계정도 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-147">You also need to have a destination storage account.</span></span> <span data-ttu-id="d299a-148">아직 없는 경우 포털(**더 많은 서비스** > 저장소 계정 > 추가) 또는 [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet을 사용하여 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-148">If you don't already have one, you can create one using either the portal (**More Services** > Storage accounts > Add) or using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="d299a-149">[AzCopy 도구](../../storage/common/storage-use-azcopy.md)를 다운로드 및 설치했습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-149">Have downloaded and installed the [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-the-vm"></a><span data-ttu-id="d299a-150">VM 할당을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-150">Deallocate the VM</span></span>
<span data-ttu-id="d299a-151">VM 할당을 취소하여 복사할 VHD를 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-151">Deallocate the VM, which frees up the VHD to be copied.</span></span> 

* <span data-ttu-id="d299a-152">**포털**: **가상 컴퓨터** > **myVM** > 중지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="d299a-153">**Powershell**: [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)을 사용하여 **myResourceGroup** 리소스 그룹에서 **myVM**으로 명명된 VM을 중지(할당 취소)합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) to stop (deallocate) the VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="d299a-154">Azure Portal의 VM에 대한 **상태**가 **중지됨**에서 **중지됨(할당 취소됨)**으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-154">The **Status** for the VM in the Azure portal changes from **Stopped** to **Stopped (deallocated)**.</span></span>

### <a name="get-the-storage-account-urls"></a><span data-ttu-id="d299a-155">저장소 계정 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="d299a-155">Get the storage account URLs</span></span>
<span data-ttu-id="d299a-156">원본 및 대상 저장소 계정의 URL이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-156">You need the URLs of the source and destination storage accounts.</span></span> <span data-ttu-id="d299a-157">URL은 `https://<storageaccount>.blob.core.windows.net/<containerName>/` 형태입니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-157">The URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="d299a-158">저장소 계정 및 컨테이너 이름을 이미 알고 있는 경우 괄호 사이의 정보를 바꿔서 URL을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-158">If you already know the storage account and container name, you can just replace the information between the brackets to create your URL.</span></span> 

<span data-ttu-id="d299a-159">Azure 포털 또는 Azure PowerShell을 사용하여 URL을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-159">You can use the Azure portal or Azure Powershell to get the URL:</span></span>

* <span data-ttu-id="d299a-160">**포털**: **>** **추가 서비스** > **저장소 계정** > *저장소 계정* > **Blob**을 클릭하면 원본 VHD 파일이 **vhds** 컨테이너에 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-160">**Portal**: Click the **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in the **vhds** container.</span></span> <span data-ttu-id="d299a-161">컨테이너의 **속성**을 클릭하고 레이블이 **URL**인 텍스트를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-161">Click **Properties** for the container, and copy the text labeled **URL**.</span></span> <span data-ttu-id="d299a-162">원본 및 대상 컨테이너의 URL이 모두 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-162">You'll need the URLs of both the source and destination containers.</span></span> 
* <span data-ttu-id="d299a-163">**Powershell**: [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm)을 사용하여 **myResourceGroup** 리소스 그룹에서 **myVM**으로 명명된 VM에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) to get the information for VM named **myVM** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="d299a-164">결과에서 **Vhd Uri**에 대한 **저장소 프로필** 섹션을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-164">In the results, look in the **Storage profile** section for the **Vhd Uri**.</span></span> <span data-ttu-id="d299a-165">Uri의 첫 번째 부분은 컨테이너에 대한 URL이고 마지막 부분은 VM에 대한 OS VHD 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-165">The first part of the Uri is the URL to the container and the last part is the OS VHD name for the VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-the-storage-access-keys"></a><span data-ttu-id="d299a-166">저장소 액세스 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="d299a-166">Get the storage access keys</span></span>
<span data-ttu-id="d299a-167">원본 및 대상 저장소 계정에 대한 액세스 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-167">Find the access keys for the source and destination storage accounts.</span></span> <span data-ttu-id="d299a-168">액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 방법](../../storage/common/storage-create-storage-account.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d299a-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="d299a-169">**포털**: **추가 서비스** > **저장소 계정** > *저장소 계정* > **액세스 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="d299a-170">**key1**로 레이블이 지정된 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-170">Copy the key labeled as **key1**.</span></span>
* <span data-ttu-id="d299a-171">**Powershell**: [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey)를 사용하여 **myResourceGroup** 리소스 그룹에서 **mystorageaccount** 저장소 계정에 대한 저장소 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) to get the storage key for the storage account **mystorageaccount** in the resource group **myResourceGroup**.</span></span> <span data-ttu-id="d299a-172">**key1**로 레이블이 지정된 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-172">Copy the key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-the-vhd"></a><span data-ttu-id="d299a-173">VHD 복사</span><span class="sxs-lookup"><span data-stu-id="d299a-173">Copy the VHD</span></span>
<span data-ttu-id="d299a-174">AzCopy를 사용하여 저장소 계정 간에 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="d299a-175">대상 컨테이너에 대해 지정된 컨테이너가 존재하지 않는 경우 컨테이너가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-175">For the destination container, if the specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="d299a-176">AzCopy를 사용하려면 로컬 컴퓨터에서 명령 프롬프트를 열고 AzCopy가 설치된 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-176">To use AzCopy, open a command prompt on your local machine and navigate to the folder where AzCopy is installed.</span></span> <span data-ttu-id="d299a-177">이 폴더는 *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-177">It will be similar to *C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="d299a-178">컨테이너 내의 모든 파일을 복사하려면 **/S** 스위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-178">To copy all of the files within a container, you use the **/S** switch.</span></span> <span data-ttu-id="d299a-179">동일한 컨테이너에 있는 경우 OS VHD 및 모든 데이터 디스크를 복사하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-179">This can be used to copy the OS VHD and all of the data disks if they are in the same container.</span></span> <span data-ttu-id="d299a-180">이 예에서는 **mysourcestorageaccount** 저장소 계정의 **mysourcecontainer** 컨테이너에 있는 모든 파일을 **mydestinationstorageaccount** 저장소 계정의 **mydestinationcontainer** 컨테이너로 복사하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-180">This example shows how to copy all of the files in the container **mysourcecontainer** in storage account **mysourcestorageaccount** to the container **mydestinationcontainer** in the **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="d299a-181">저장소 계정 및 컨테이너의 이름을 사용자 고유 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-181">Replace the names of the storage accounts and containers with your own.</span></span> <span data-ttu-id="d299a-182">`<sourceStorageAccountKey1>` 및 `<destinationStorageAccountKey1>`을 사용자 고유 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="d299a-183">여러 파일과 함께 컨테이너에서 특정 VHD를 복사하려면 /Pattern 스위치를 사용하여 파일 이름을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-183">If you only want to copy a specific VHD in a container with multiple files, you can also specify the file name using the /Pattern switch.</span></span> <span data-ttu-id="d299a-184">이 예에서는 **myFileName.vhd**라는 파일만 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-184">In this example, only the file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="d299a-185">완료되면 다음과 유사한 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-185">When it is finished, you will get a message that looks something like:</span></span>

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a><span data-ttu-id="d299a-186">문제 해결</span><span class="sxs-lookup"><span data-stu-id="d299a-186">Troubleshooting</span></span>
* <span data-ttu-id="d299a-187">AZCopy를 사용하는 경우 “서버가 요청을 인증하지 못했습니다.”라는 오류 메시지가 표시되면 권한 부여 헤더의 값이 서명을 포함하여 올바른 형식으로 지정되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-187">When you use AZCopy, if you see the error "Server failed to authenticate the request", make sure the value of the Authorization header is formed correctly including the signature.</span></span> <span data-ttu-id="d299a-188">키 2 또는 보조 저장소 키를 사용 중인 경우 주 또는 첫 번째 저장소 키를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="d299a-188">If you are using Key 2 or the secondary storage key, try using the primary or 1st storage key.</span></span>

## <a name="create-the-new-vm"></a><span data-ttu-id="d299a-189">새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="d299a-189">Create the new VM</span></span> 

<span data-ttu-id="d299a-190">새 VM에서 사용할 네트워킹 및 기타 VM 리소스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-190">You need to create networking and other VM resources to be used by the new VM.</span></span>

### <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="d299a-191">서브넷 및 VNet 만들기</span><span class="sxs-lookup"><span data-stu-id="d299a-191">Create the subNet and vNet</span></span>

<span data-ttu-id="d299a-192">[가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 VNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-192">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="d299a-193">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-193">Create the subNet.</span></span> <span data-ttu-id="d299a-194">이 예제에서는 **myResourceGroup** 리소스 그룹에 **mySubNet**으로 명명된 서브넷을 만들고 **10.0.0.0/24**에 대한 서브넷 주소 접두사를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-194">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="d299a-195">VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-195">Create the vNet.</span></span> <span data-ttu-id="d299a-196">이 예제에서는 가상 네트워크 이름을 **myVnetName**으로, 위치를 **미국 서부**로, 가상 네트워크의 주소 접두사를 **10.0.0.0/16**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-196">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="d299a-197">공용 IP 주소 및 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="d299a-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="d299a-198">가상 네트워크에서 가상 컴퓨터와 통신하려면 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-198">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="d299a-199">공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-199">Create the public IP.</span></span> <span data-ttu-id="d299a-200">이 예제에서는 공용 IP 주소 이름을 **myIP**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-200">In this example, the public IP address name is set to **myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="d299a-201">NIC 만들기.</span><span class="sxs-lookup"><span data-stu-id="d299a-201">Create the NIC.</span></span> <span data-ttu-id="d299a-202">이 예제에서는 NIC 이름을 **myNicName**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-202">In this example, the NIC name is set to **myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="d299a-203">네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="d299a-203">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="d299a-204">RDP를 사용하여 VM에 로그인할 수 있으려면 포트 3389에 대한 RDP 액세스를 허용하는 보안 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-204">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="d299a-205">새 VM의 VHD가 기존의 특수한 VM에서 생성되었기 때문에 VM이 만들어진 후에 RDP를 사용하여 로그온할 사용 권한을 갖고 있던 원본 가상 컴퓨터에서 기존 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-205">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span></span>
<span data-ttu-id="d299a-206">이 예제에서는 NSG 이름을 **myNsg**로 설정하고 RDP 규칙 이름을 **myRdpRule**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-206">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="d299a-207">끝점 및 NSG 규칙에 대한 자세한 내용은 [PowerShell을 사용하여 Azure에서 VM으로 포트 열기](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d299a-207">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-the-vm-name-and-size"></a><span data-ttu-id="d299a-208">VM 이름 및 크기 설정</span><span class="sxs-lookup"><span data-stu-id="d299a-208">Set the VM name and size</span></span>

<span data-ttu-id="d299a-209">이 예에서는 VM 이름을 "myVM"으로 설정하고 VM 크기를 "Standard_A2"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-209">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-the-nic"></a><span data-ttu-id="d299a-210">NIC 추가</span><span class="sxs-lookup"><span data-stu-id="d299a-210">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-the-os-disk"></a><span data-ttu-id="d299a-211">OS 디스크 구성</span><span class="sxs-lookup"><span data-stu-id="d299a-211">Configure the OS disk</span></span>

1. <span data-ttu-id="d299a-212">업로드하거나 복사한 VHD의 URI를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-212">Set the URI for the VHD that you uploaded or copied.</span></span> <span data-ttu-id="d299a-213">이 예에서는 **myOsDisk.vhd**라는 VHD 파일을 **myContainer**라는 컨테이너의 **myStorageAccount**라는 저장소 계정에 보관합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-213">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="d299a-214">OS 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-214">Add the OS disk.</span></span> <span data-ttu-id="d299a-215">이 예에서는 OS 디스크가 만들어지면 VM 이름에 "osDisk"가 추가되어 OS 디스크 이름이 완성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-215">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span></span> <span data-ttu-id="d299a-216">또한 이 예에서는 이 Windows 기반 VHD를 VM에 OS 디스크로 연결해야 하는 것으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-216">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="d299a-217">선택 사항: VM에 연결해야 하는 데이터 디스크가 있는 경우 데이터 VHD의 URL과 적절한 LUN(논리 단위 번호)을 사용하여 데이터 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-217">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="d299a-218">저장소 계정을 사용하는 경우 데이터 및 운영 체제 디스크 URL은 `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd` 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-218">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="d299a-219">포털에서 대상 저장소 컨테이너로 이동하고 운영 체제 또는 복사된 데이터 VHD를 클릭한 다음 URL의 내용을 복사하여 이 내용을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-219">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span></span>


### <a name="complete-the-vm"></a><span data-ttu-id="d299a-220">VM 완료</span><span class="sxs-lookup"><span data-stu-id="d299a-220">Complete the VM</span></span> 

<span data-ttu-id="d299a-221">방금 만든 구성을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-221">Create the VM using the configurations that we just created.</span></span>

```powershell
#Create the new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="d299a-222">이 명령에 성공할 경우 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="d299a-223">VM이 만들어졌는지 확인</span><span class="sxs-lookup"><span data-stu-id="d299a-223">Verify that the VM was created</span></span>
<span data-ttu-id="d299a-224">새로 만든 VM은 [Azure Portal](https://portal.azure.com)에서 **찾아보기** > **가상 컴퓨터**에 표시되며 다음 PowerShell 명령을 사용해도 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-224">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="d299a-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d299a-225">Next steps</span></span>
<span data-ttu-id="d299a-226">새 가상 컴퓨터에 로그인하려면 [포털](https://portal.azure.com)에서 VM으로 이동한 다음 **연결**을 클릭하고 원격 데스크톱 RDP 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-226">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="d299a-227">원본 가상 컴퓨터의 계정 자격 증명을 사용하여 새 가상 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="d299a-227">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="d299a-228">자세한 내용은 [Windows를 실행하는 Azure 가상 컴퓨터에 연결하고 로그온하는 방법](connect-logon.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d299a-228">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

