---
title: "Azure에서 일반화된 VHD를 업로드하여 여러 VM 만들기 | Microsoft Docs"
description: "Azure Storage 계정에 일반화된 VHD를 업로드하여 Resource Manager 배포 모델과 함께 사용할 Windows VM을 만듭니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: e6fc49855b449a7723a7f8a0c1c41516b3a44ee5
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="upload-a-generalized-vhd-to-azure-to-create-a-new-vm"></a><span data-ttu-id="0eab0-103">Azure에 일반화된 VHD를 업로드하여 새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0eab0-103">Upload a generalized VHD to Azure to create a new VM</span></span>

<span data-ttu-id="0eab0-104">이 항목에서는 일반화된 관리되지 않는 디스크를 저장소 계정에 업로드한 다음 업로드된 디스크를 사용하여 새 VM을 만드는 방법에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-104">This topic covers uploading a generalized unmanaged disk to a storage account and then creating a new VM using the uploaded disk.</span></span> <span data-ttu-id="0eab0-105">일반화된 VHD 이미지에는 Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-105">A generalized VHD image has had all of your personal account information removed using Sysprep.</span></span> 

<span data-ttu-id="0eab0-106">저장소 계정의 전문화된 VHD에서 VM을 만들려는 경우 [전문화된 VHD에서 VM 만들기](sa-create-vm-specialized.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eab0-106">If you want to create a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](sa-create-vm-specialized.md).</span></span>

<span data-ttu-id="0eab0-107">이 항목에서는 저장소 계정을 사용하지만 고객은 대신 Managed Disks를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-107">This topic covers using storage accounts, but we recommend customers move to using Managed Disks instead.</span></span> <span data-ttu-id="0eab0-108">관리 디스크를 사용하여 새 VM을 준비, 업로드 및 만드는 방법에 대한 전체 연습을 보려면 [Managed Disks를 사용하여 Azure에 업로드된 일반화된 VHD에서 새 VM 만들기](upload-generalized-managed.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eab0-108">For a complete walk-through of how to prepare, upload and create a new VM using managed disks, see [Create a new VM from a generalized VHD uploaded to Azure using Managed Disks](upload-generalized-managed.md).</span></span>



## <a name="prepare-the-vm"></a><span data-ttu-id="0eab0-109">VM 준비</span><span class="sxs-lookup"><span data-stu-id="0eab0-109">Prepare the VM</span></span>

<span data-ttu-id="0eab0-110">일반화된 VHD에는 Sysprep을 사용하여 제거된 모든 개인 계정 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-110">A generalized VHD has had all of your personal account information removed using Sysprep.</span></span> <span data-ttu-id="0eab0-111">새 VM을 만드는 이미지로 VHD를 사용하려는 경우 다음을 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-111">If you intend to use the VHD as an image to create new VMs from, you should:</span></span>
  
  * <span data-ttu-id="0eab0-112">[Azure에 업로드할 Windows VHD를 준비합니다](prepare-for-upload-vhd-image.md).</span><span class="sxs-lookup"><span data-stu-id="0eab0-112">[Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md).</span></span> 
  * <span data-ttu-id="0eab0-113">Sysprep을 사용하여 가상 컴퓨터를 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-113">Generalize the virtual machine using Sysprep</span></span>

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a><span data-ttu-id="0eab0-114">Sysprep을 사용하여 Windows 가상 컴퓨터 일반화</span><span class="sxs-lookup"><span data-stu-id="0eab0-114">Generalize a Windows virtual machine using Sysprep</span></span>
<span data-ttu-id="0eab0-115">이 섹션에서는 이미지로 사용하기 위해 Windows 가상 컴퓨터를 일반화하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-115">This section shows you how to generalize your Windows virtual machine for use as an image.</span></span> <span data-ttu-id="0eab0-116">Sysprep은 여러 정보 중에서 모든 개인 계정 정보를 제거하고 이미지로 사용할 컴퓨터를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-116">Sysprep removes all your personal account information, among other things, and prepares the machine to be used as an image.</span></span> <span data-ttu-id="0eab0-117">Sysprep에 대한 자세한 내용은 [Sysprep 사용 방법: 소개](http://technet.microsoft.com/library/bb457073.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eab0-117">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="0eab0-118">가상 컴퓨터에서 실행되는 서버 역할이 Sysprep에서 지원되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-118">Make sure the server roles running on the machine are supported by Sysprep.</span></span> <span data-ttu-id="0eab0-119">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="0eab0-119">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0eab0-120">Azure에 VHD를 업로드하기 전에 Sysprep을 처음으로 실행하는 경우 Sysprep을 실행하기 전에 [VM을 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-120">If you are running Sysprep before uploading your VHD to Azure for the first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="0eab0-121">Windows 가상 컴퓨터에 로그인</span><span class="sxs-lookup"><span data-stu-id="0eab0-121">Sign in to the Windows virtual machine.</span></span>
2. <span data-ttu-id="0eab0-122">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-122">Open the Command Prompt window as an administrator.</span></span> <span data-ttu-id="0eab0-123">디렉터리를 **%windir%\system32\sysprep**로 변경한 후 `sysprep.exe`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-123">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="0eab0-124">**시스템 준비 도구** 대화 상자에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화** 확인란을 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-124">In the **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that the **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="0eab0-125">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-125">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="0eab0-126">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-126">Click **OK**.</span></span>
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="0eab0-128">Sysprep이 완료되면 가상 컴퓨터를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-128">When Sysprep completes, it shuts down the virtual machine.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="0eab0-129">Azure에 VHD를 업로드하거나 VM에서 이미지를 만드는 작업을 완료할 때까지 VM을 다시 시작하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-129">Do not restart the VM until you are done uploading the VHD to Azure or creating an image from the VM.</span></span> <span data-ttu-id="0eab0-130">VM이 실수로 다시 시작되면 Sysprep을 실행하여 다시 일반화합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-130">If the VM accidentally gets restarted, run Sysprep to generalize it again.</span></span>
> 
> 


## <a name="upload-the-vhd"></a><span data-ttu-id="0eab0-131">VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="0eab0-131">Upload the VHD</span></span>

<span data-ttu-id="0eab0-132">Azure Storage 계정에 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="0eab0-132">Upload the VHD to an Azure storage account.</span></span>

### <a name="log-in-to-azure"></a><span data-ttu-id="0eab0-133">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="0eab0-133">Log in to Azure</span></span>
<span data-ttu-id="0eab0-134">PowerShell 버전 1.4 이상을 아직 설치하지 않은 경우 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eab0-134">If you don't already have PowerShell version 1.4 or above installed, read [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="0eab0-135">Azure PowerShell을 열고 Azure 계정에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-135">Open Azure PowerShell and sign in to your Azure account.</span></span> <span data-ttu-id="0eab0-136">Azure 계정 자격 증명을 입력하기 위한 팝업 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-136">A pop-up window opens for you to enter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="0eab0-137">사용 가능한 구독에 대한 구독을 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-137">Get the subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="0eab0-138">구독 ID를 사용하여 올바른 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-138">Set the correct subscription using the subscription ID.</span></span> <span data-ttu-id="0eab0-139">`<subscriptionID>`를 올바른 구독의 ID로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-139">Replace `<subscriptionID>` with the ID of the correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-the-storage-account"></a><span data-ttu-id="0eab0-140">저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="0eab0-140">Get the storage account</span></span>
<span data-ttu-id="0eab0-141">업로드한 VM 이미지를 저장할 Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-141">You need a storage account in Azure to store the uploaded VM image.</span></span> <span data-ttu-id="0eab0-142">기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-142">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="0eab0-143">사용 가능한 저장소 계정을 표시하려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-143">To show the available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="0eab0-144">기존 저장소 계정을 사용하려면 [VM 이미지 업로드](#upload-the-vm-vhd-to-your-storage-account) 섹션을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-144">If you want to use an existing storage account, proceed to the [Upload the VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="0eab0-145">저장소 계정을 만들어야 하는 경우 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-145">If you need to create a storage account, follow these steps:</span></span>

1. <span data-ttu-id="0eab0-146">저장소 계정을 만들어야 하는 리소스 그룹의 이름을 알아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-146">You need the name of the resource group where the storage account should be created.</span></span> <span data-ttu-id="0eab0-147">구독의 모든 리소스 그룹을 찾으려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-147">To find out all the resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="0eab0-148">**미국 서부** 지역에 **myResourceGroup** 이라는 이름의 리소스 그룹을 만들려면 다음을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-148">To create a resource group named **myResourceGroup** in the **West US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. <span data-ttu-id="0eab0-149">[New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet을 사용하여 이 리소스 그룹에 **mystorageaccount**라는 이름의 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-149">Create a storage account named **mystorageaccount** in this resource group by using the [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-the-upload"></a><span data-ttu-id="0eab0-150">업로드 시작</span><span class="sxs-lookup"><span data-stu-id="0eab0-150">Start the upload</span></span> 

<span data-ttu-id="0eab0-151">[Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet을 사용하여 저장소 계정의 컨테이너에 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-151">Use the [Add-AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet to upload the image to a container in your storage account.</span></span> <span data-ttu-id="0eab0-152">이 예제에서는 `"C:\Users\Public\Documents\Virtual hard disks\"`에서 **myResourceGroup** 리소스 그룹의 **mystorageaccount**라는 저장소 계정에 파일 **myVHD.vhd**를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-152">This example uploads the file **myVHD.vhd** from `"C:\Users\Public\Documents\Virtual hard disks\"` to a storage account named **mystorageaccount** in the **myResourceGroup** resource group.</span></span> <span data-ttu-id="0eab0-153">파일은 **mycontainer**라는 컨테이너에 배치되고 새 파일 이름은 **myUploadedVHD.vhd**가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-153">The file will be placed into the container named **mycontainer** and the new file name will be **myUploadedVHD.vhd**.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="0eab0-154">성공하면 다음과 유사한 응답을 얻게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-154">If successful, you get a response that looks similar to this:</span></span>

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

<span data-ttu-id="0eab0-155">이 명령은 네트워크 연결 및 VHD 파일의 크기에 따라 완료하는 데 다소 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-155">Depending on your network connection and the size of your VHD file, this command may take a while to complete.</span></span>


## <a name="create-a-new-vm"></a><span data-ttu-id="0eab0-156">새 VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0eab0-156">Create a new VM</span></span> 

<span data-ttu-id="0eab0-157">이제 업로드된 VHD를 사용하여 새 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-157">You can now use the uploaded VHD to create a new VM.</span></span> 

### <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="0eab0-158">VHD의 URI 설정</span><span class="sxs-lookup"><span data-stu-id="0eab0-158">Set the URI of the VHD</span></span>

<span data-ttu-id="0eab0-159">VHD에 대한 URI는 형식: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="0eab0-159">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="0eab0-160">이 예에서는 **myVHD**로 명명된 VHD가 **mycontainer** 컨테이너의 **mystorageaccount** 저장소 계정에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-160">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a><span data-ttu-id="0eab0-161">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="0eab0-161">Create a virtual network</span></span>
<span data-ttu-id="0eab0-162">[가상 네트워크](../../virtual-network/virtual-networks-overview.md)의 vNet 및 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-162">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="0eab0-163">서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-163">Create the subnet.</span></span> <span data-ttu-id="0eab0-164">다음 예제에서는 **10.0.0.0/24** 주소 접두사가 있는 **myResourceGroup** 리소스 그룹에 **mySubnet**으로 명명된 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-164">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="0eab0-165">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="0eab0-165">Create the virtual network.</span></span> <span data-ttu-id="0eab0-166">다음 예제에서는 **10.0.0.0/16** 주소 접두사가 있는 **미국 서부** 위치에 **myVnet**으로 명명된 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-166">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="0eab0-167">공용 IP 주소 및 네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="0eab0-167">Create a public IP address and network interface</span></span>
<span data-ttu-id="0eab0-168">가상 네트워크에서 가상 컴퓨터와 통신하려면 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-168">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="0eab0-169">공용 IP 주소 만들기.</span><span class="sxs-lookup"><span data-stu-id="0eab0-169">Create a public IP address.</span></span> <span data-ttu-id="0eab0-170">이 예에서는 **myPip**라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-170">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="0eab0-171">NIC 만들기.</span><span class="sxs-lookup"><span data-stu-id="0eab0-171">Create the NIC.</span></span> <span data-ttu-id="0eab0-172">이 예에서는 **myNic**라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-172">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="0eab0-173">네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="0eab0-173">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="0eab0-174">RDP를 사용하여 VM에 로그인할 수 있으려면 포트 3389에 대한 RDP 액세스를 허용하는 보안 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-174">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="0eab0-175">이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 **myRdpRule**이라는 규칙을 포함하는 **myNsg**로 명명된 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-175">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="0eab0-176">NSG에 대한 자세한 내용은 [PowerShell을 사용하여 Azure에서 VM으로 포트 열기](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eab0-176">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="0eab0-177">가상 네트워크에 대한 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="0eab0-177">Create a variable for the virtual network</span></span>
<span data-ttu-id="0eab0-178">완료된 가상 네트워크에 대한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-178">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-the-vm"></a><span data-ttu-id="0eab0-179">VM 만들기</span><span class="sxs-lookup"><span data-stu-id="0eab0-179">Create the VM</span></span>
<span data-ttu-id="0eab0-180">다음 PowerShell 스크립트는 가상 컴퓨터 구성을 설정하고 업로드된 VM 이미지를 새 설치에 대한 소스로 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-180">The following PowerShell script shows how to set up the virtual machine configurations and use the uploaded VM image as the source for the new installation.</span></span>



```powershell
# Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="0eab0-181">VM이 만들어졌는지 확인</span><span class="sxs-lookup"><span data-stu-id="0eab0-181">Verify that the VM was created</span></span>
<span data-ttu-id="0eab0-182">완료되면 새로 만든 VM은 [Azure 포털](https://portal.azure.com)에서 **찾아보기** > **가상 컴퓨터**에 표시되며 다음 PowerShell 명령을 사용해도 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0eab0-182">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="0eab0-183">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0eab0-183">Next steps</span></span>
<span data-ttu-id="0eab0-184">Azure PowerShell을 사용하여 새 가상 컴퓨터를 관리하려면 [Azure Resource Manager 및 PowerShell을 사용하여 가상 컴퓨터 관리](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0eab0-184">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


