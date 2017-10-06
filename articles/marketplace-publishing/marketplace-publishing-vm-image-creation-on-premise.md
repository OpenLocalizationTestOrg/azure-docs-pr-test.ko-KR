---
title: "Azure 마켓플레이스 hello에 대 한 온-프레미스 가상 컴퓨터 이미지 aaaCreating | Microsoft Docs"
description: "이해 및 hello 단계 toocreate 온-프레미스 VM 이미지를 실행 하 고 다른 사용자에 대 한 Azure 마켓플레이스 toohello 배포 toopurchase 합니다."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a><span data-ttu-id="9491f-103">Azure 마켓플레이스 hello에 대 한 온-프레미스 가상 컴퓨터 이미지를 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-103">Develop an on-premises virtual machine image for hello Azure Marketplace</span></span>
<span data-ttu-id="9491f-104">원격 데스크톱 프로토콜을 사용 하 여 hello 클라우드에서 직접 Azure 가상 하드 디스크 (Vhd)를 개발 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-104">We strongly recommend that you develop Azure virtual hard disks (VHDs) directly in hello cloud by using Remote Desktop Protocol.</span></span> <span data-ttu-id="9491f-105">그러나 필요한 경우 가능한 toodownload VHD 이며 온-프레미스 인프라를 사용 하 여 개발 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-105">However, if you must, it is possible toodownload a VHD and develop it by using on-premises infrastructure.</span></span>  

<span data-ttu-id="9491f-106">온-프레미스 개발의 경우 hello 운영 체제의 hello 만든 VHD를 다운로드 해야 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-106">For on-premises development, you must download hello operating system VHD of hello created VM.</span></span> <span data-ttu-id="9491f-107">다음 단계는 위의 3.3단계의 일부로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-107">These steps would take place as part of step 3.3, above.</span></span>  

## <a name="download-a-vhd-image"></a><span data-ttu-id="9491f-108">VHD 이미지 다운로드</span><span class="sxs-lookup"><span data-stu-id="9491f-108">Download a VHD image</span></span>
### <a name="locate-a-blob-url"></a><span data-ttu-id="9491f-109">Blob URL 찾기</span><span class="sxs-lookup"><span data-stu-id="9491f-109">Locate a blob URL</span></span>
<span data-ttu-id="9491f-110">순서 toodownload hello VHD에서 먼저 hello 운영 체제 디스크에 대 한 hello blob URL를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-110">In order toodownload hello VHD, first locate hello blob URL for hello operating system disk.</span></span>

<span data-ttu-id="9491f-111">새 hello에서 hello blob URL을 찾을 [Microsoft Azure 포털](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="9491f-111">Locate hello blob URL from hello new [Microsoft Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="9491f-112">너무 이동**찾아보기** > **Vm**를 선택한 후 hello VM을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-112">Go too**Browse** > **VMs**, and then select hello deployed VM.</span></span>
2. <span data-ttu-id="9491f-113">**구성**선택, hello **디스크** 타일을 hello 디스크 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-113">Under **Configure**, select hello **Disks** tile, which opens hello Disks blade.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. <span data-ttu-id="9491f-115">선택 hello **OS 디스크**, hello VHD 위치를 포함 하 여 디스크 속성을 표시 하는 다른 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-115">Select hello **OS Disk**, which opens another blade that displays disk properties, including hello VHD location.</span></span>
4. <span data-ttu-id="9491f-116">이 Blob URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-116">Copy this blob URL.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. <span data-ttu-id="9491f-118">이제 삭제 hello hello 백업 디스크를 삭제 하지 않고 VM을 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-118">Now, delete hello deployed VM without deleting hello backing disks.</span></span> <span data-ttu-id="9491f-119">삭제 하는 대신 hello VM을 중지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-119">You can also stop hello VM instead of deleting it.</span></span> <span data-ttu-id="9491f-120">Hello VM에서 실행 중인 경우에 hello 운영 체제 VHD를 다운로드 하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9491f-120">Do not download hello operating system VHD when hello VM is running.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a><span data-ttu-id="9491f-122">VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="9491f-122">Download a VHD</span></span>
<span data-ttu-id="9491f-123">Hello blob URL을 알고 있다면 후 hello를 사용 하 여 hello VHD를 다운로드할 수 있습니다 [Azure 포털](http://manage.windowsazure.com/) 또는 PowerShell입니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-123">After you know hello blob URL, you can download hello VHD by using hello [Azure portal](http://manage.windowsazure.com/) or PowerShell.</span></span>  

> [!NOTE]
> <span data-ttu-id="9491f-124">이 가이드의이 만들기의 hello 시 hello 기능 toodownload VHD 아직 없으면 hello 새 Microsoft Azure 포털에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-124">At hello time of this guide’s creation, hello functionality toodownload a VHD is not yet present in hello new Microsoft Azure portal.</span></span>  
> 
> 

<span data-ttu-id="9491f-125">**현재 hello 통해 hello 운영 체제 VHD 다운로드 [Azure 포털](http://manage.windowsazure.com/)**</span><span class="sxs-lookup"><span data-stu-id="9491f-125">**Download hello operating system VHD via hello current [Azure portal](http://manage.windowsazure.com/)**</span></span>

1. <span data-ttu-id="9491f-126">하지 않았으면 지금 이미 경우 toohello Azure 포털에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-126">Sign in toohello Azure portal if you have not done so already.</span></span>
2. <span data-ttu-id="9491f-127">Hello 클릭 **저장소** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-127">Click hello **Storage** tab.</span></span>
3. <span data-ttu-id="9491f-128">저장 된 VHD는 hello 내 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-128">Select hello storage account within which hello VHD is stored.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. <span data-ttu-id="9491f-130">그러면 저장소 계정 속성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-130">This displays storage account properties.</span></span> <span data-ttu-id="9491f-131">선택 hello **컨테이너** 탭 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-131">Select hello **Containers** tab.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. <span data-ttu-id="9491f-133">hello에 VHD 저장 되는 hello 컨테이너를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-133">Select hello container in which hello VHD is stored.</span></span> <span data-ttu-id="9491f-134">기본적으로 hello 포털에서 만든 VHD hello vhd 컨테이너에 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-134">By default, when created from hello portal, hello VHD is stored in a vhds container.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. <span data-ttu-id="9491f-136">Hello URL toohello 저장 하나 비교 하 여 hello 올바른 운영 체제 VHD를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-136">Select hello correct operating system VHD by comparing hello URL toohello one you saved.</span></span>
7. <span data-ttu-id="9491f-137">**다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-137">Click **Download**.</span></span>
   
   ![그리기](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a><span data-ttu-id="9491f-139">PowerShell을 사용하여 VHD 다운로드</span><span class="sxs-lookup"><span data-stu-id="9491f-139">Download a VHD by using PowerShell</span></span>
<span data-ttu-id="9491f-140">또한 toousing hello Azure 포털, hello를 사용할 수 있습니다 [Save-azurevhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello 운영 체제 VHD입니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-140">In addition toousing hello Azure portal, you can use hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload hello operating system VHD.</span></span>

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
<span data-ttu-id="9491f-141">예: Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span><span class="sxs-lookup"><span data-stu-id="9491f-141">For example, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String></span></span>

> [!NOTE]
> <span data-ttu-id="9491f-142">**Save-azurevhd** 역시는 **NumberOfThreads** 수 있는 옵션이 hello 다운로드용 tooincrease 병렬 처리 수준 toomake hello 사용에 가장 적합 사용 가능한 대역폭을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-142">**Save-AzureVhd** also has a **NumberOfThreads** option that can be used tooincrease parallelism toomake hello best use of available bandwidth for hello download.</span></span>
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a><span data-ttu-id="9491f-143">Vhd tooan Azure 저장소 계정에 업로드</span><span class="sxs-lookup"><span data-stu-id="9491f-143">Upload VHDs tooan Azure storage account</span></span>
<span data-ttu-id="9491f-144">Vhd 온-프레미스를 준비 해야 tooupload 저장소로 azure에서 계정.</span><span class="sxs-lookup"><span data-stu-id="9491f-144">If you prepared your VHDs on-premises, you need tooupload them into a storage account in Azure.</span></span> <span data-ttu-id="9491f-145">이 단계는 온-프레미스에서 VHD를 만든 후, VM 이미지에 대한 인증을 가져오기 전에 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-145">This step takes place after creating your VHD on-premises but before obtaining certification for your VM image.</span></span>

### <a name="create-a-storage-account-and-container"></a><span data-ttu-id="9491f-146">저장소 계정 및 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="9491f-146">Create a storage account and container</span></span>
<span data-ttu-id="9491f-147">Hello 미국에 있는 영역에서 저장소 계정에 Vhd를 업로드 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-147">We recommend that VHDs be uploaded into a storage account in a region in hello United States.</span></span> <span data-ttu-id="9491f-148">단일 SKU에 대한 모든 VHD는 단일 저장소 계정 내에서 단일 컨테이너에 배치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-148">All VHDs for a single SKU should be placed in a single container within a single storage account.</span></span>

<span data-ttu-id="9491f-149">저장소 계정 toocreate hello를 사용할 수 있습니다 [Microsoft Azure 포털](https://portal.azure.com/), PowerShell 또는 hello Linux 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-149">toocreate a storage account, you can use hello [Microsoft Azure portal](https://portal.azure.com/), PowerShell, or hello Linux command-line tool.</span></span>  

<span data-ttu-id="9491f-150">**Hello Microsoft Azure 포털에서 저장소 계정을 만들려면**</span><span class="sxs-lookup"><span data-stu-id="9491f-150">**Create a storage account from hello Microsoft Azure portal**</span></span>

1. <span data-ttu-id="9491f-151">**새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-151">Click **New**.</span></span>
2. <span data-ttu-id="9491f-152">**저장소**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-152">Select **Storage**.</span></span>
3. <span data-ttu-id="9491f-153">Hello 저장소 계정 이름에 채운 다음 위치를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-153">Fill in hello storage account name, and then select a location.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. <span data-ttu-id="9491f-155">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-155">Click **Create**.</span></span>
5. <span data-ttu-id="9491f-156">저장소 계정을 만든 hello에 대 한 hello 블레이드 열려 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-156">hello blade for hello created storage account should be open.</span></span> <span data-ttu-id="9491f-157">그렇지 않은 경우 **찾아보기** > **저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-157">If not, select **Browse** > **Storage Accounts**.</span></span> <span data-ttu-id="9491f-158">계정 블레이드 hello 저장소에서 만든 hello 저장소 계정을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-158">On hello Storage account blade, select hello storage account created.</span></span>
6. <span data-ttu-id="9491f-159">**컨테이너**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-159">Select **Containers**.</span></span>
   
   ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. <span data-ttu-id="9491f-161">Hello 컨테이너 블레이드에서 선택 **추가**를 컨테이너 이름 및 hello 컨테이너 권한을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-161">On hello Containers blade, select **Add**, and then enter a container name and hello container permissions.</span></span> <span data-ttu-id="9491f-162">컨테이너 권한에 대해 **개인** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-162">Select **Private** for container permissions.</span></span>

> [!TIP]
> <span data-ttu-id="9491f-163">Toopublish를 계획 하는 SKU 당 하나의 컨테이너를 만들어야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-163">We recommend that you create one container per SKU that you are planning toopublish.</span></span>
> 
> 

  ![drawing](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a><span data-ttu-id="9491f-165">PowerShell을 사용하여 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="9491f-165">Create a storage account by using PowerShell</span></span>
<span data-ttu-id="9491f-166">Hello를 사용 하 여 저장소 계정을 만드는 PowerShell을 사용 하 여 [새로 AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9491f-166">Using PowerShell, create a storage account by using hello [New-AzureStorageAccount](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.</span></span>

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

<span data-ttu-id="9491f-167">그러면 hello를 사용 하 여 해당 저장소 계정 내의 컨테이너를 만들 수 있습니다 [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9491f-167">Then you can create a container within that storage account by using hello [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.</span></span>

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> <span data-ttu-id="9491f-168">이러한 명령이 PowerShell에서 이미 설정 되어 해당 hello 현재 저장소 계정 컨텍스트를 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-168">Those commands assume that hello current storage account context has already been set in PowerShell.</span></span>   <span data-ttu-id="9491f-169">너무 참조[Azure PowerShell을 설정](marketplace-publishing-powershell-setup.md) PowerShell 설치에 대 한 자세한 내용은 합니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-169">Refer too[Setting up Azure PowerShell](marketplace-publishing-powershell-setup.md) for more details on PowerShell setup.</span></span>  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="9491f-170">Mac 및 Linux 용 hello 명령줄 도구를 사용 하 여 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="9491f-170">Create a storage account by using hello command-line tool for Mac and Linux</span></span>
> <span data-ttu-id="9491f-171">[Linux 명령줄 도구](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 다음과 같이 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-171">From [Linux command-line tool](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), create a storage account as follows.</span></span>
> 
> 

        azure storage account create mystorageaccount --location "West US"

<span data-ttu-id="9491f-172">다음과 같이 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-172">Create a container as follows.</span></span>

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a><span data-ttu-id="9491f-173">VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="9491f-173">Upload a VHD</span></span>
<span data-ttu-id="9491f-174">Hello 저장소 계정 및 컨테이너를 만든 후에 준비 된 Vhd를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-174">After hello storage account and container are created, you can upload your prepared VHDs.</span></span> <span data-ttu-id="9491f-175">PowerShell, hello Linux 명령줄 도구 또는 기타 Azure 저장소 관리 도구를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9491f-175">You can use PowerShell, hello Linux command-line tool, or other Azure Storage management tools.</span></span>

### <a name="upload-a-vhd-via-powershell"></a><span data-ttu-id="9491f-176">PowerShell 통해 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="9491f-176">Upload a VHD via PowerShell</span></span>
<span data-ttu-id="9491f-177">사용 하 여 hello [Add-azurevhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9491f-177">Use hello [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.</span></span>

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a><span data-ttu-id="9491f-178">Mac 및 Linux 용 hello 명령줄 도구를 사용 하 여 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="9491f-178">Upload a VHD by using hello command-line tool for Mac and Linux</span></span>
<span data-ttu-id="9491f-179">Hello로 [Linux 명령줄 도구](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), hello 다음 이름을 사용해 서: azure vm 이미지 만들기 <image name> -위치 <Location of hello data center> -OS Linux<LocationOfLocalVHD></span><span class="sxs-lookup"><span data-stu-id="9491f-179">With hello [Linux command-line tool](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use hello following: azure vm image create <image name> --location <Location of hello data center> --OS Linux <LocationOfLocalVHD></span></span>

## <a name="see-also"></a><span data-ttu-id="9491f-180">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9491f-180">See also</span></span>
* [<span data-ttu-id="9491f-181">마켓플레이스 hello에 대 한 가상 컴퓨터 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="9491f-181">Creating a virtual machine image for hello Marketplace</span></span>](marketplace-publishing-vm-image-creation.md)
* [<span data-ttu-id="9491f-182">Azure PowerShell 설정</span><span class="sxs-lookup"><span data-stu-id="9491f-182">Setting up Azure PowerShell</span></span>](marketplace-publishing-powershell-setup.md)

