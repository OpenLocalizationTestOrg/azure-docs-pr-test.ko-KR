---
title: "Azure에서 특수 한 디스크에서 VM aaaCreate | Microsoft Docs"
description: "Hello 리소스 관리자 배포 모델에서 관리 되지 않는 특수 한 디스크를 연결 하 여 새 VM을 만듭니다."
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
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a><span data-ttu-id="cea68-103">저장소 계정의 특수한 VHD에서 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="cea68-103">Create a VM from a specialized VHD in a storage account</span></span>

<span data-ttu-id="cea68-104">Powershell을 사용 하 여 hello 운영 체제 디스크와 관리 되지 않는 특수 한 디스크를 연결 하 여 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-104">Create a new VM by attaching a specialized unmanaged disk as hello OS disk using Powershell.</span></span> <span data-ttu-id="cea68-105">특수 한 디스크는 hello 사용자 계정, 응용 프로그램 및 원래 VM에서 다른 상태 데이터를 유지 하는 기존 VM에서 VHD의 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-105">A specialized disk is a copy of VHD from an existing VM that maintains hello user accounts, applications and other state data from your original VM.</span></span> 

<span data-ttu-id="cea68-106">다음 두 가지 옵션을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-106">You have two options:</span></span>
* [<span data-ttu-id="cea68-107">VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="cea68-107">Upload a VHD</span></span>](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [<span data-ttu-id="cea68-108">Hello 기존 Azure VM의 VHD를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-108">Copy hello VHD of an existing Azure VM</span></span>](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a><span data-ttu-id="cea68-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="cea68-109">Before you begin</span></span>
<span data-ttu-id="cea68-110">PowerShell을 사용 하는 경우 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="cea68-111">실행 명령 tooinstall 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-111">Run hello following command tooinstall it.</span></span>

```powershell
Install-Module AzureRM.Compute 
```
<span data-ttu-id="cea68-112">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cea68-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="option-1-upload-a-specialized-vhd"></a><span data-ttu-id="cea68-113">옵션 1: 특수한 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="cea68-113">Option 1: Upload a specialized VHD</span></span>

<span data-ttu-id="cea68-114">Hello 하이퍼-V 또는 VM 사설 클라우드에서 다른 클라우드에서 내보낼 처럼 온-프레미스 가상화 도구를 사용 하 여 만든 특수 한 VM에서 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-114">You can upload hello VHD from a specialized VM created with an on-premises virtualization tool, like Hyper-V, or a VM exported from another cloud.</span></span>

### <a name="prepare-hello-vm"></a><span data-ttu-id="cea68-115">Hello VM 준비</span><span class="sxs-lookup"><span data-stu-id="cea68-115">Prepare hello VM</span></span>
<span data-ttu-id="cea68-116">온-프레미스 VM을 사용하여 만든 특수한 VHD 또는 다른 클라우드에서 내보낸 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-116">You can upload a specialized VHD that was created using an on-premises VM or a VHD exported from another cloud.</span></span> <span data-ttu-id="cea68-117">특수화 된 VHD hello 사용자 계정, 응용 프로그램 및 원래 VM에서 다른 상태 데이터를 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-117">A specialized VHD maintains hello user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="cea68-118">Toouse를 가져오려는 경우 VHD로 hello-toocreate 새 VM은 hello 다음 단계를 완료 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-118">If you intend toouse hello VHD as-is toocreate a new VM, ensure hello following steps are completed.</span></span> 
  
  * <span data-ttu-id="cea68-119">[Windows VHD tooupload tooAzure 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-119">[Prepare a Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="cea68-120">**없는** 일반화 Sysprep를 사용 하 여 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-120">**Do not** generalize hello VM using Sysprep.</span></span>
  * <span data-ttu-id="cea68-121">모든 게스트 가상화 도구와 hello (즉, VMware 도구)를 VM에 설치 된 에이전트를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-121">Remove any guest virtualization tools and agents that are installed on hello VM (i.e. VMware tools).</span></span>
  * <span data-ttu-id="cea68-122">Hello VM 확인 해당 IP 주소 및 DNS 설정이 DHCP 통해 구성 된 toopull 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-122">Ensure hello VM is configured toopull its IP address and DNS settings via DHCP.</span></span> <span data-ttu-id="cea68-123">이렇게 하면 해당 hello 서버를 시작할 때 hello VNet 내에서 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-123">This ensures that hello server obtains an IP address within hello VNet when it starts up.</span></span> 


### <a name="get-hello-storage-account"></a><span data-ttu-id="cea68-124">Hello 저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="cea68-124">Get hello storage account</span></span>
<span data-ttu-id="cea68-125">Azure toostore 업로드 hello VM 이미지에 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-125">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="cea68-126">기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-126">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="cea68-127">tooshow hello 사용 가능한 저장소 계정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-127">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="cea68-128">Toouse 기존 저장소 계정을 사용할 경우 진행 toohello [hello VM 이미지 업로드](#upload-the-vm-vhd-to-your-storage-account) 섹션.</span><span class="sxs-lookup"><span data-stu-id="cea68-128">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="cea68-129">저장소 계정 toocreate 해야 할 경우 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="cea68-129">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="cea68-130">Hello 저장소 계정을 만들어야 하는 hello 리소스 그룹의 hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-130">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="cea68-131">구독을 형식에 있는 모든 hello 리소스 그룹 아웃 toofind:</span><span class="sxs-lookup"><span data-stu-id="cea68-131">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="cea68-132">리소스 그룹 이름이 toocreate **myResourceGroup** hello에 **미국 서 부** 지역, 유형:</span><span class="sxs-lookup"><span data-stu-id="cea68-132">toocreate a resource group named **myResourceGroup** in hello **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="cea68-133">라는 저장소 계정 만들기 **mystorageaccount** hello를 사용 하 여이 리소스 그룹에 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cea68-133">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="cea68-134">Hello VHD tooyour 저장소 계정에 업로드</span><span class="sxs-lookup"><span data-stu-id="cea68-134">Upload hello VHD tooyour storage account</span></span>
<span data-ttu-id="cea68-135">사용 하 여 hello [추가 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) 저장소 계정의 cmdlet tooupload hello 이미지 tooa 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-135">Use hello [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello image tooa container in your storage account.</span></span> <span data-ttu-id="cea68-136">이 예에서는 업로드 파일 hello **myVHD.vhd** 에서 `"C:\Users\Public\Documents\Virtual hard disks\"` tooa 저장소 계정인 **mystorageaccount** hello에 **myResourceGroup** 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-136">This example uploads hello file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` tooa storage account named **mystorageaccount** in hello **myResourceGroup** resource group.</span></span> <span data-ttu-id="cea68-137">hello 파일 라는 hello 컨테이너에 배치 됨 **mycontainer** hello 새 파일 이름이 됩니다 **myUploadedVHD.vhd**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-137">hello file will be placed into hello container named **mycontainer** and hello new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="cea68-138">성공 하면 다음과 비슷한 toothis 응답 가져오기:</span><span class="sxs-lookup"><span data-stu-id="cea68-138">If successful, you get a response that looks similar toothis:</span></span>

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

<span data-ttu-id="cea68-139">이 명령은 네트워크 연결 및 VHD 파일의 hello 크기에 따라 시간이 걸릴 수 있습니다 toocomplete 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-139">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete.</span></span>


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a><span data-ttu-id="cea68-140">옵션 2: 기존 Azure VM에서 hello VHD를 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-140">Option 2: Copy hello VHD from an existing Azure VM</span></span>

<span data-ttu-id="cea68-141">새, 중복 된 VM을 만들 때 VHD tooanother 저장소 계정 toouse를 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-141">You can copy a VHD tooanother storage account toouse when creating a new, duplicate VM.</span></span>

### <a name="before-you-begin"></a><span data-ttu-id="cea68-142">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="cea68-142">Before you begin</span></span>
<span data-ttu-id="cea68-143">다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-143">Make sure that you:</span></span>

* <span data-ttu-id="cea68-144">Hello에 대 한 정보가 **원본 및 대상 저장소 계정**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-144">Have information about hello **source and destination storage accounts**.</span></span> <span data-ttu-id="cea68-145">Hello 원본 VM toohave hello 저장소 계정 및 컨테이너 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-145">For hello source VM, you need toohave hello storage account and container names.</span></span> <span data-ttu-id="cea68-146">Hello 컨테이너 이름이 됩니다 일반적으로 **vhd**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-146">Usually, hello container name will be **vhds**.</span></span> <span data-ttu-id="cea68-147">대상 저장소 계정 toohave를 해야합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-147">You also need toohave a destination storage account.</span></span> <span data-ttu-id="cea68-148">아직 없는 하나, 각 hello 포털을 사용 하 여 하나를 만들 수 있습니다 (**더 서비스** > 저장소 계정 > 추가) 또는 hello를 사용 하 여 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cea68-148">If you don't already have one, you can create one using either hello portal (**More Services** > Storage accounts > Add) or using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet.</span></span> 
* <span data-ttu-id="cea68-149">다운로드 하 고 hello 설치한 [AzCopy tool](../../storage/common/storage-use-azcopy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-149">Have downloaded and installed hello [AzCopy tool](../../storage/common/storage-use-azcopy.md).</span></span> 

### <a name="deallocate-hello-vm"></a><span data-ttu-id="cea68-150">Hello VM 할당 취소</span><span class="sxs-lookup"><span data-stu-id="cea68-150">Deallocate hello VM</span></span>
<span data-ttu-id="cea68-151">Hello 복사 hello VHD toobe 확보 하는 VM 할당이 취소 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-151">Deallocate hello VM, which frees up hello VHD toobe copied.</span></span> 

* <span data-ttu-id="cea68-152">**포털**: **가상 컴퓨터** > **myVM** > 중지를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-152">**Portal**: Click **Virtual machines** > **myVM** > Stop</span></span>
* <span data-ttu-id="cea68-153">**Powershell**: 사용 [중지 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (할당 취소) 가상 컴퓨터 V hello **myVM** 리소스 그룹에 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-153">**Powershell**: Use [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop (deallocate) hello VM named **myVM** in resource group **myResourceGroup**.</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="cea68-154">hello **상태** hello Azure에에서 VM hello에 대 한 포털에서 변경 **Stopped** 너무**중지 됨 (할당 취소 됨)**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-154">hello **Status** for hello VM in hello Azure portal changes from **Stopped** too**Stopped (deallocated)**.</span></span>

### <a name="get-hello-storage-account-urls"></a><span data-ttu-id="cea68-155">Hello 저장소 계정 Url 가져오기</span><span class="sxs-lookup"><span data-stu-id="cea68-155">Get hello storage account URLs</span></span>
<span data-ttu-id="cea68-156">Hello Url의 hello 원본 및 대상 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-156">You need hello URLs of hello source and destination storage accounts.</span></span> <span data-ttu-id="cea68-157">hello Url 같이: `https://<storageaccount>.blob.core.windows.net/<containerName>/`합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-157">hello URLs look like: `https://<storageaccount>.blob.core.windows.net/<containerName>/`.</span></span> <span data-ttu-id="cea68-158">Hello 저장소 계정 및 컨테이너 이름을 알고 있는 경우 hello 대괄호 toocreate 간에 hello 정보를 URL만 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-158">If you already know hello storage account and container name, you can just replace hello information between hello brackets toocreate your URL.</span></span> 

<span data-ttu-id="cea68-159">Hello Azure 포털 또는 Azure Powershell tooget hello URL을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-159">You can use hello Azure portal or Azure Powershell tooget hello URL:</span></span>

* <span data-ttu-id="cea68-160">**포털**: hello 클릭  **>**  에 대 한 **더 많은 서비스** > **저장소 계정은**  >   *저장소 계정* > **Blob** 원본 VHD 파일 hello 되었 및 **vhd** 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-160">**Portal**: Click hello **>** for **More services** > **Storage accounts** > *storage account* > **Blobs** and your source VHD file is probably in hello **vhds** container.</span></span> <span data-ttu-id="cea68-161">클릭 **속성** hello 컨테이너 및 hello 텍스트 레이블이 지정 된 복사에 대 한 **URL**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-161">Click **Properties** for hello container, and copy hello text labeled **URL**.</span></span> <span data-ttu-id="cea68-162">원본과 대상 모두 hello 컨테이너의 hello Url 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-162">You'll need hello URLs of both hello source and destination containers.</span></span> 
* <span data-ttu-id="cea68-163">**Powershell**: 사용 [Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) 이라는 VM에 대 한 tooget hello 정보 **myVM** hello 리소스 그룹에 **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-163">**Powershell**: Use [Get-AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm) tooget hello information for VM named **myVM** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="cea68-164">Hello 찾는 위치 hello 결과에 **저장소 프로필** hello에 대 한 섹션 **Vhd Uri**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-164">In hello results, look in hello **Storage profile** section for hello **Vhd Uri**.</span></span> <span data-ttu-id="cea68-165">hello Uri의 첫 번째 부분 hello hello URL toohello 컨테이너 고 hello 마지막 부분은 hello hello VM에 대 한 운영 체제 VHD 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-165">hello first part of hello Uri is hello URL toohello container and hello last part is hello OS VHD name for hello VM.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a><span data-ttu-id="cea68-166">Hello 저장소 액세스 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="cea68-166">Get hello storage access keys</span></span>
<span data-ttu-id="cea68-167">원본 및 대상 저장소 계정이 hello에 대 한 hello 선택 키를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-167">Find hello access keys for hello source and destination storage accounts.</span></span> <span data-ttu-id="cea68-168">액세스 키에 대한 자세한 내용은 [Azure 저장소 계정 방법](../../storage/common/storage-create-storage-account.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cea68-168">For more information about access keys, see [About Azure storage accounts](../../storage/common/storage-create-storage-account.md).</span></span>

* <span data-ttu-id="cea68-169">**포털**: **추가 서비스** > **저장소 계정** > *저장소 계정* > **액세스 키**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-169">**Portal**: Click **More services** > **Storage accounts** > *storage account* > **Access keys**.</span></span> <span data-ttu-id="cea68-170">로 표시 된 hello 키 복사 **key1**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-170">Copy hello key labeled as **key1**.</span></span>
* <span data-ttu-id="cea68-171">**Powershell**: 사용 [Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello 저장소 계정에 대 한 저장소 키를 hello **mystorageaccount** hello 리소스 그룹에  **myResourceGroup**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-171">**Powershell**: Use [Get-AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello storage key for hello storage account **mystorageaccount** in hello resource group **myResourceGroup**.</span></span> <span data-ttu-id="cea68-172">레이블이 지정 된 hello 키 복사 **key1**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-172">Copy hello key labeled **key1**.</span></span>

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a><span data-ttu-id="cea68-173">Hello VHD 복사</span><span class="sxs-lookup"><span data-stu-id="cea68-173">Copy hello VHD</span></span>
<span data-ttu-id="cea68-174">AzCopy를 사용하여 저장소 계정 간에 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-174">You can copy files between storage accounts using AzCopy.</span></span> <span data-ttu-id="cea68-175">Hello 대상 컨테이너에 대 한 지정 된 컨테이너 hello 존재 하지 않으면 자동으로 만들어집니다 드립니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-175">For hello destination container, if hello specified container doesn't exist, it will be created for you.</span></span> 

<span data-ttu-id="cea68-176">toouse AzCopy 로컬 컴퓨터에서 명령 프롬프트를 열고 AzCopy를 설치한 toohello 폴더를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-176">toouse AzCopy, open a command prompt on your local machine and navigate toohello folder where AzCopy is installed.</span></span> <span data-ttu-id="cea68-177">너무 비슷한 됩니다*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-177">It will be similar too*C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy*.</span></span> 

<span data-ttu-id="cea68-178">hello를 사용 하면 toocopy hello의 모든 컨테이너 내에서 파일을 **/S** 전환 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-178">toocopy all of hello files within a container, you use hello **/S** switch.</span></span> <span data-ttu-id="cea68-179">이 사용 되는 toocopy hello OS VHD 수와 동일한 컨테이너 hello 모든 hello 데이터 디스크에 있는 경우에 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-179">This can be used toocopy hello OS VHD and all of hello data disks if they are in hello same container.</span></span> <span data-ttu-id="cea68-180">이 예에서는 어떻게 hello 컨테이너의 모든 hello 파일 toocopy **mysourcecontainer** 저장소 계정에 **mysourcestorageaccount** toohello 컨테이너 **mydestinationcontainer**  hello에 **mydestinationstorageaccount** 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-180">This example shows how toocopy all of hello files in hello container **mysourcecontainer** in storage account **mysourcestorageaccount** toohello container **mydestinationcontainer** in hello **mydestinationstorageaccount** storage account.</span></span> <span data-ttu-id="cea68-181">사용자의 정보로 hello hello 저장소 계정 이름 및 컨테이너를 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-181">Replace hello names of hello storage accounts and containers with your own.</span></span> <span data-ttu-id="cea68-182">`<sourceStorageAccountKey1>` 및 `<destinationStorageAccountKey1>`을 사용자 고유 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-182">Replace `<sourceStorageAccountKey1>` and `<destinationStorageAccountKey1>` with your own keys.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

<span data-ttu-id="cea68-183">여러 파일 toocopy 컨테이너에서 특정 VHD만 하려는 경우 또한 hello /Pattern 스위치를 사용 하 여 hello 파일 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-183">If you only want toocopy a specific VHD in a container with multiple files, you can also specify hello file name using hello /Pattern switch.</span></span> <span data-ttu-id="cea68-184">이 예제에서는 라는 파일만 hello **myFileName.vhd** 복사 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-184">In this example, only hello file named **myFileName.vhd** will be copied.</span></span>

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


<span data-ttu-id="cea68-185">완료되면 다음과 유사한 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-185">When it is finished, you will get a message that looks something like:</span></span>

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

### <a name="troubleshooting"></a><span data-ttu-id="cea68-186">문제 해결</span><span class="sxs-lookup"><span data-stu-id="cea68-186">Troubleshooting</span></span>
* <span data-ttu-id="cea68-187">를 사용 하면 AZCopy hello 오류가 나타나는 경우 "tooauthenticate hello 요청 하지 못했습니다 서버" 올바르게 hello 서명을 포함 하 여 hello hello 권한 부여 헤더 값의 형식이 설정 되어 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-187">When you use AZCopy, if you see hello error "Server failed tooauthenticate hello request", make sure hello value of hello Authorization header is formed correctly including hello signature.</span></span> <span data-ttu-id="cea68-188">키 2 또는 hello 보조 저장소 키를 사용 하는 경우 hello 주 또는 1 일 저장소 키를 사용해 보세요.</span><span class="sxs-lookup"><span data-stu-id="cea68-188">If you are using Key 2 or hello secondary storage key, try using hello primary or 1st storage key.</span></span>

## <a name="create-hello-new-vm"></a><span data-ttu-id="cea68-189">만들 새 VM hello</span><span class="sxs-lookup"><span data-stu-id="cea68-189">Create hello new VM</span></span> 

<span data-ttu-id="cea68-190">Toocreate 네트워킹 및 hello에서 사용 하는 다른 VM 리소스 toobe 해야 새 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-190">You need toocreate networking and other VM resources toobe used by hello new VM.</span></span>

### <a name="create-hello-subnet-and-vnet"></a><span data-ttu-id="cea68-191">Hello 서브넷 및 vNet 만들기</span><span class="sxs-lookup"><span data-stu-id="cea68-191">Create hello subNet and vNet</span></span>

<span data-ttu-id="cea68-192">Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-192">Create hello vNet and subNet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="cea68-193">Hello 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-193">Create hello subNet.</span></span> <span data-ttu-id="cea68-194">이 예에서는 이라는 서브넷을 만듭니다 **mySubNet**, hello 리소스 그룹에 **myResourceGroup**, 집합 서브넷 주소 접두사를 너무 hello 및**10.0.0.0/24**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-194">This example creates a subnet named **mySubNet**, in hello resource group **myResourceGroup**, and sets hello subnet address prefix too**10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="cea68-195">Hello vNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-195">Create hello vNet.</span></span> <span data-ttu-id="cea68-196">이 예제에서는 집합에 가상 네트워크 이름 toobe hello **myVnetName**, 위치를 너무 hello**미국 서 부**, hello 가상 네트워크에 대 한 주소 접두사를 너무 hello 및**10.0.0.0/16**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-196">This example sets hello virtual network name toobe **myVnetName**, hello location too**West US**, and hello address prefix for hello virtual network too**10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="cea68-197">공용 IP 주소 및 NIC 만들기</span><span class="sxs-lookup"><span data-stu-id="cea68-197">Create a public IP address and NIC</span></span>
<span data-ttu-id="cea68-198">필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="cea68-198">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="cea68-199">Hello 공용 IP를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-199">Create hello public IP.</span></span> <span data-ttu-id="cea68-200">이 예제에서는 hello 공용 IP 주소 이름이 설정 되어 너무**myIP**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-200">In this example, hello public IP address name is set too**myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="cea68-201">Hello NIC. 만들기</span><span class="sxs-lookup"><span data-stu-id="cea68-201">Create hello NIC.</span></span> <span data-ttu-id="cea68-202">이 예제에서는 hello NIC 이름이 설정 되어 너무**myNicName**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-202">In this example, hello NIC name is set too**myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="cea68-203">Hello 네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="cea68-203">Create hello network security group and an RDP rule</span></span>
<span data-ttu-id="cea68-204">toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 보안 규칙이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-204">toobe able toolog in tooyour VM using RDP, you need toohave an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="cea68-205">기존에서 새 VM을 만든 hello에 대 한 VHD hello 특수화 되므로 VM, 있습니다 hello VM 만들어진 후 hello 원본 가상 컴퓨터에 RDP를 사용 하 여 권한 toolog에서 기존 계정을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-205">Because hello VHD for hello new VM was created from an existing specialized VM, after hello VM is created you can use an existing account from hello source virtual machine that had permission toolog on using RDP.</span></span>
<span data-ttu-id="cea68-206">이 예제에서는 집합 hello NSG 이름을 너무**myNsg** 너무 hello RDP 규칙 이름 및**myRdpRule**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-206">This example sets hello NSG name too**myNsg** and hello RDP rule name too**myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="cea68-207">끝점 및 NSG 규칙에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-207">For more information about endpoints and NSG rules, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="set-hello-vm-name-and-size"></a><span data-ttu-id="cea68-208">Hello VM 이름 및 크기를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-208">Set hello VM name and size</span></span>

<span data-ttu-id="cea68-209">이 예제에서는 집합에 VM 이름 hello 너무 "myVM" 및 hello VM 크기가 너무 "Standard_A2"입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-209">This example sets hello VM name too"myVM" and hello VM size too"Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a><span data-ttu-id="cea68-210">Hello NIC를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-210">Add hello NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a><span data-ttu-id="cea68-211">Hello OS 디스크 구성</span><span class="sxs-lookup"><span data-stu-id="cea68-211">Configure hello OS disk</span></span>

1. <span data-ttu-id="cea68-212">Hello 업로드 또는 복사 된 VHD에 대 한 hello URI를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-212">Set hello URI for hello VHD that you uploaded or copied.</span></span> <span data-ttu-id="cea68-213">이 예제에서는 명명 된 VHD 파일을 hello **myOsDisk.vhd** 라는 저장소 계정에 유지 되는 **myStorageAccount** 라는 컨테이너에 **myContainer**합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-213">In this example, hello VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="cea68-214">Hello OS 디스크를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-214">Add hello OS disk.</span></span> <span data-ttu-id="cea68-215">이 예제에서는 hello OS 디스크를 만들면 osDisk"hello 용어" appened toohello VM 이름 toocreate hello OS 디스크 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-215">In this example, when hello OS disk is created, hello term "osDisk" is appened toohello VM name toocreate hello OS disk name.</span></span> <span data-ttu-id="cea68-216">또한이 Windows 기반 VHD 연결된 toohello hello OS 디스크로 VM 되어야 함을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-216">This example also specifies that this Windows-based VHD should be attached toohello VM as hello OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="cea68-217">선택 사항: 데이터 디스크가 있는 경우 해당 필요 toobe 연결 된 VM toohello hello 데이터 디스크를 사용 하 여 hello 데이터 Vhd의 Url 및 적절 한 논리 단위 번호 (Lun) hello를 추가 하세요.</span><span class="sxs-lookup"><span data-stu-id="cea68-217">Optional: If you have data disks that need toobe attached toohello VM, add hello data disks by using hello URLs of data VHDs and hello appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="cea68-218">저장소 계정을 사용할 경우, hello 데이터 및 운영 체제 디스크 Url이 다음과 같은: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-218">When using a storage account, hello data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="cea68-219">Hello 운영 체제 또는 데이터 복사 된 VHD 클릭 하면 toohello 대상 저장소 컨테이너를 찾아보고 다음 hello URL의 hello 내용을 복사 하 여 hello 포털에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-219">You can find this on hello portal by browsing toohello target storage container, clicking hello operating system or data VHD that was copied, and then copying hello contents of hello URL.</span></span>


### <a name="complete-hello-vm"></a><span data-ttu-id="cea68-220">전체 hello VM</span><span class="sxs-lookup"><span data-stu-id="cea68-220">Complete hello VM</span></span> 

<span data-ttu-id="cea68-221">만들 방금 만든 hello 구성을 사용 하 여 VM hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-221">Create hello VM using hello configurations that we just created.</span></span>

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="cea68-222">이 명령에 성공할 경우 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-222">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="cea68-223">VM이 생성 되었고 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-223">Verify that hello VM was created</span></span>
<span data-ttu-id="cea68-224">Hello 새로 만든 VM hello에 표시 되어야 [Azure 포털](https://portal.azure.com)아래 **찾아보기** > **가상 컴퓨터**, 또는 다음 PowerShell hello를 사용 하 여 명령:</span><span class="sxs-lookup"><span data-stu-id="cea68-224">You should see hello newly created VM either in hello [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="cea68-225">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cea68-225">Next steps</span></span>
<span data-ttu-id="cea68-226">tooyour 새 가상 컴퓨터, hello에 찾아보기 toohello VM에에서 toosign [포털](https://portal.azure.com), 클릭 **연결**, 및 열기 hello RDP 원격 데스크톱 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-226">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="cea68-227">Tooyour 새 가상 컴퓨터에 프로그램 원래 가상 컴퓨터 toosign의 hello 계정 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-227">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="cea68-228">자세한 내용은 참조 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cea68-228">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md).</span></span>

