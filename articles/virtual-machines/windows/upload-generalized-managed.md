---
title: "일반화 된 온-프레미스 VHD에서 관리 되는 Azure VM aaaCreate | Microsoft Docs"
description: "일반화 된 VHD tooAzure 업로드 하 고 toocreate 사용 hello 리소스 관리자 배포 모델에서 새 Vm입니다."
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
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a><span data-ttu-id="56386-103">일반화 된 VHD를 업로드 하 고 toocreate를 사용 하 여 Azure에서 새 Vm</span><span class="sxs-lookup"><span data-stu-id="56386-103">Upload a generalized VHD and use it toocreate new VMs in Azure</span></span>

<span data-ttu-id="56386-104">이 항목에서는 PowerShell tooupload를 사용 하 여 일반화 된 VM tooAzure의 VHD, hello VHD에서에서 이미지 만들기 및 해당 이미지에서 새 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56386-104">This topic walks you through using PowerShell tooupload a VHD of a generalized VM tooAzure, create an image from hello VHD and create a new VM from that image.</span></span> <span data-ttu-id="56386-105">다른 클라우드 또는 온-프레미스 가상화 도구에서 내보낸 VHD를 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56386-105">You can upload a VHD exported from an on-premises virtualization tool or from another cloud.</span></span> <span data-ttu-id="56386-106">사용 하 여 [관리 하는 디스크](managed-disks-overview.md) hello에 대 한 새 VM hello VM 관리를 단순화 하 고 hello VM은 가용성 집합에 배치 하는 경우 더 나은 가용성을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-106">Using [Managed Disks](managed-disks-overview.md) for hello new VM simplifies hello VM managment and provides better availability when hello VM is placed in an availability set.</span></span> 

<span data-ttu-id="56386-107">샘플 스크립트 toouse 참조 [스크립트 tooupload VHD tooAzure 샘플링 및 새 VM 만들기](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span><span class="sxs-lookup"><span data-stu-id="56386-107">If you want toouse a sample script, see [Sample script tooupload a VHD tooAzure and create a new VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="56386-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="56386-108">Before you begin</span></span>

- <span data-ttu-id="56386-109">모든 VHD tooAzure를 업로드 하기 전에 따라야 [Windows VHD 또는 VHDX tooupload tooAzure 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="56386-109">Before uploading any VHD tooAzure, you should follow [Prepare a Windows VHD or VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="56386-110">검토 [hello 마이그레이션 계획 tooManaged 디스크](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) 너무 마이그레이션을 시작 하기 전에[관리 하는 디스크](managed-disks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-110">Review [Plan for hello migration tooManaged Disks](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks) before starting your migration too[Managed Disks](managed-disks-overview.md).</span></span>
- <span data-ttu-id="56386-111">Hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-111">Make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="56386-112">실행 명령 tooinstall 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-112">Run hello following command tooinstall it.</span></span>

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    <span data-ttu-id="56386-113">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="56386-113">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="generalize-hello-windows-vm-using-sysprep"></a><span data-ttu-id="56386-114">일반화 hello Sysprep를 사용 하 여 Windows VM</span><span class="sxs-lookup"><span data-stu-id="56386-114">Generalize hello Windows VM using Sysprep</span></span>

<span data-ttu-id="56386-115">Sysprep는 특히, 모든 개인 계정 정보를 제거 하 고 이미지 형식으로 사용 되는 hello 컴퓨터 toobe를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-115">Sysprep removes all your personal account information, among other things, and prepares hello machine toobe used as an image.</span></span> <span data-ttu-id="56386-116">Sysprep에 대 한 세부 정보를 참조 하십시오. [어떻게 tooUse Sysprep: 소개](http://technet.microsoft.com/library/bb457073.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-116">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span>

<span data-ttu-id="56386-117">Hello 컴퓨터에서 실행 되는 hello 서버 역할과 Sysprep에서 사용할 수 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-117">Make sure hello server roles running on hello machine are supported by Sysprep.</span></span> <span data-ttu-id="56386-118">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span><span class="sxs-lookup"><span data-stu-id="56386-118">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="56386-119">를 사용 하 여 VHD tooAzure hello에 대 한 처음으로 업로드 하기 전에 Sysprep를 실행 하는 경우 했는지 확인 [VM 준비](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Sysprep를 실행 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="56386-119">If you are running Sysprep before uploading your VHD tooAzure for hello first time, make sure you have [prepared your VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before running Sysprep.</span></span> 
> 
> 

1. <span data-ttu-id="56386-120">Windows 가상 컴퓨터 toohello에 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-120">Sign in toohello Windows virtual machine.</span></span>
2. <span data-ttu-id="56386-121">Hello 명령 프롬프트 창을 관리자 권한으로 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56386-121">Open hello Command Prompt window as an administrator.</span></span> <span data-ttu-id="56386-122">Hello 디렉터리도 변경**%windir%\system32\sysprep**, 한 다음 실행 `sysprep.exe`합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-122">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>
3. <span data-ttu-id="56386-123">Hello에 **시스템 준비 도구** 대화 상자에서 **입력 시스템을 기본 OOBE (Experience)**, 해당 hello 있는지 확인 하 고 **일반화** 확인란을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-123">In hello **System Preparation Tool** dialog box, select **Enter System Out-of-Box Experience (OOBE)**, and make sure that hello **Generalize** check box is selected.</span></span>
4. <span data-ttu-id="56386-124">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-124">In **Shutdown Options**, select **Shutdown**.</span></span>
5. <span data-ttu-id="56386-125">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-125">Click **OK**.</span></span>
   
    ![Sysprep 시작](./media/upload-generalized-managed/sysprepgeneral.png)
6. <span data-ttu-id="56386-127">Sysprep이 완료 된 hello 가상 컴퓨터를 종료 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-127">When Sysprep completes, it shuts down hello virtual machine.</span></span> <span data-ttu-id="56386-128">Hello VM을 다시 시작 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56386-128">Do not restart hello VM.</span></span>



## <a name="log-in-tooazure"></a><span data-ttu-id="56386-129">TooAzure 로그인</span><span class="sxs-lookup"><span data-stu-id="56386-129">Log in tooAzure</span></span>
<span data-ttu-id="56386-130">PowerShell 버전 1.4가 없는 이상 읽기 설치 [어떻게 tooinstall Azure PowerShell을 구성 하 고](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-130">If you don't already have PowerShell version 1.4 or above installed, read [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

1. <span data-ttu-id="56386-131">Azure PowerShell을 열고 tooyour Azure 계정에에서 로그인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-131">Open Azure PowerShell and sign in tooyour Azure account.</span></span> <span data-ttu-id="56386-132">Azure 계정 자격을 증명 tooenter 있습니다에 대 한 팝업 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="56386-132">A pop-up window opens for you tooenter your Azure account credentials.</span></span>
   
    ```powershell
    Login-AzureRmAccount
    ```
2. <span data-ttu-id="56386-133">사용 가능한 구독에 대 한 hello 구독을 Id를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="56386-133">Get hello subscription IDs for your available subscriptions.</span></span>
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. <span data-ttu-id="56386-134">Hello 구독 id입니다.를 사용 하 여 hello 올바른 구독 설정</span><span class="sxs-lookup"><span data-stu-id="56386-134">Set hello correct subscription using hello subscription ID.</span></span> <span data-ttu-id="56386-135">대체  *<subscriptionID>*  hello hello ID로 구독을 수정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-135">Replace *<subscriptionID>* with hello ID of hello correct subscription.</span></span>
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a><span data-ttu-id="56386-136">Hello 저장소 계정 가져오기</span><span class="sxs-lookup"><span data-stu-id="56386-136">Get hello storage account</span></span>
<span data-ttu-id="56386-137">Azure toostore 업로드 hello VM 이미지에 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-137">You need a storage account in Azure toostore hello uploaded VM image.</span></span> <span data-ttu-id="56386-138">기존 저장소 계정을 사용하거나 새 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56386-138">You can either use an existing storage account or create a new one.</span></span> 

<span data-ttu-id="56386-139">사용 하려는 hello VHD toocreate 관리 디스크 vm의 경우, hello 저장소 계정 위치 hello VM 만들어야 하는 동일한 hello 위치를 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-139">If you will be using hello VHD toocreate a managed disk for a VM, hello storage account location must be same hello location where you will be creating hello VM.</span></span>

<span data-ttu-id="56386-140">tooshow hello 사용 가능한 저장소 계정을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-140">tooshow hello available storage accounts, type:</span></span>

```powershell
Get-AzureRmStorageAccount
```

<span data-ttu-id="56386-141">Toouse 기존 저장소 계정을 사용할 경우 진행 toohello [hello VM 이미지 업로드](#upload-the-vm-vhd-to-your-storage-account) 섹션.</span><span class="sxs-lookup"><span data-stu-id="56386-141">If you want toouse an existing storage account, proceed toohello [Upload hello VM image](#upload-the-vm-vhd-to-your-storage-account) section.</span></span>

<span data-ttu-id="56386-142">저장소 계정 toocreate 해야 할 경우 다음이 단계를 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="56386-142">If you need toocreate a storage account, follow these steps:</span></span>

1. <span data-ttu-id="56386-143">Hello 저장소 계정을 만들어야 하는 hello 리소스 그룹의 hello 이름이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-143">You need hello name of hello resource group where hello storage account should be created.</span></span> <span data-ttu-id="56386-144">구독을 형식에 있는 모든 hello 리소스 그룹 아웃 toofind:</span><span class="sxs-lookup"><span data-stu-id="56386-144">toofind out all hello resource groups that are in your subscription, type:</span></span>
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    <span data-ttu-id="56386-145">리소스 그룹 이름이 toocreate **myResourceGroup** hello에 **미국 동부** 지역, 유형:</span><span class="sxs-lookup"><span data-stu-id="56386-145">toocreate a resource group named **myResourceGroup** in hello **East US** region, type:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. <span data-ttu-id="56386-146">라는 저장소 계정 만들기 **mystorageaccount** hello를 사용 하 여이 리소스 그룹에 [새로 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="56386-146">Create a storage account named **mystorageaccount** in this resource group by using hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:</span></span>
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    <span data-ttu-id="56386-147">-SkuName에 대한 유효한 값은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="56386-147">Valid values for -SkuName are:</span></span>
   
   * <span data-ttu-id="56386-148">**Standard_LRS** - 로컬 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="56386-148">**Standard_LRS** - Locally redundant storage.</span></span> 
   * <span data-ttu-id="56386-149">**Standard_ZRS** - 영역 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="56386-149">**Standard_ZRS** - Zone redundant storage.</span></span>
   * <span data-ttu-id="56386-150">**Standard_GRS** - 지역 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="56386-150">**Standard_GRS** - Geo redundant storage.</span></span> 
   * <span data-ttu-id="56386-151">**Standard_RAGRS** - 읽기 액세스 지역 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="56386-151">**Standard_RAGRS** - Read access geo redundant storage.</span></span> 
   * <span data-ttu-id="56386-152">**Premium_LRS** - 프리미엄 로컬 중복 저장소</span><span class="sxs-lookup"><span data-stu-id="56386-152">**Premium_LRS** - Premium locally redundant storage.</span></span> 

## <a name="upload-hello-vhd-tooyour-storage-account"></a><span data-ttu-id="56386-153">Hello VHD tooyour 저장소 계정에 업로드</span><span class="sxs-lookup"><span data-stu-id="56386-153">Upload hello VHD tooyour storage account</span></span>

<span data-ttu-id="56386-154">사용 하 여 hello [추가 AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) 저장소 계정의 cmdlet tooupload hello VHD tooa 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="56386-154">Use hello [Add-AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa container in your storage account.</span></span> <span data-ttu-id="56386-155">이 예에서는 업로드 파일 hello *myVHD.vhd* 에서 *"C:\Users\Public\Documents\Virtual 하드 디스크\"*  tooa 저장소 계정인 *mystorageaccount*hello에 *myResourceGroup* 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="56386-155">This example uploads hello file *myVHD.vhd* from *"C:\Users\Public\Documents\Virtual hard disks\"* tooa storage account named *mystorageaccount* in hello *myResourceGroup* resource group.</span></span> <span data-ttu-id="56386-156">hello 파일 라는 hello 컨테이너에 배치 됨 *mycontainer* hello 새 파일 이름이 됩니다 *myUploadedVHD.vhd*합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-156">hello file will be placed into hello container named *mycontainer* and hello new file name will be *myUploadedVHD.vhd*.</span></span>

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


<span data-ttu-id="56386-157">성공 하면 다음과 비슷한 toothis 응답 가져오기:</span><span class="sxs-lookup"><span data-stu-id="56386-157">If successful, you get a response that looks similar toothis:</span></span>

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

<span data-ttu-id="56386-158">이 명령은 네트워크 연결 및 VHD 파일의 hello 크기에 따라 시간이 걸릴 수 있습니다 toocomplete</span><span class="sxs-lookup"><span data-stu-id="56386-158">Depending on your network connection and hello size of your VHD file, this command may take a while toocomplete</span></span>

<span data-ttu-id="56386-159">Hello 저장 **대상 URI** 경로 toouse hello를 사용 하 여 새 VM에 VHD 업로드 또는 관리 되는 디스크 toocreate 하려는 경우 이후입니다.</span><span class="sxs-lookup"><span data-stu-id="56386-159">Save hello **Destination URI** path toouse later if you are going toocreate a managed disk or a new VM using hello uploaded VHD.</span></span>

### <a name="other-options-for-uploading-a-vhd"></a><span data-ttu-id="56386-160">VHD를 업로드하기 위한 기타 옵션</span><span class="sxs-lookup"><span data-stu-id="56386-160">Other options for uploading a VHD</span></span>
 
 
<span data-ttu-id="56386-161">Hello 다음 중 하나를 사용 하 여 VHD tooyour 저장소 계정을 업로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56386-161">You can also upload a VHD tooyour storage account using one of hello following:</span></span>

- [<span data-ttu-id="56386-162">AZCopy</span><span class="sxs-lookup"><span data-stu-id="56386-162">AzCopy</span></span>](http://aka.ms/downloadazcopy)
- [<span data-ttu-id="56386-163">Azure 저장소 Blob 복사 API</span><span class="sxs-lookup"><span data-stu-id="56386-163">Azure Storage Copy Blob API</span></span>](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [<span data-ttu-id="56386-164">Azure Storage 탐색기 Blob 업로드</span><span class="sxs-lookup"><span data-stu-id="56386-164">Azure Storage Explorer Uploading Blobs</span></span>](https://azurestorageexplorer.codeplex.com/)
- [<span data-ttu-id="56386-165">저장소 가져오기/내보내기 서비스 REST API 참조</span><span class="sxs-lookup"><span data-stu-id="56386-165">Storage Import/Export Service REST API Reference</span></span>](https://msdn.microsoft.com/library/dn529096.aspx)
-   <span data-ttu-id="56386-166">예상 업로드 시간이 7일보다 긴 경우 가져오기/내보내기 서비스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56386-166">We recommend using Import/Export Service if estimated uploading time is longer than 7 days.</span></span> <span data-ttu-id="56386-167">사용할 수 있습니다 [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) 데이터 크기와 전송 단위에서 tooestimate hello 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="56386-167">You can use [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello time from data size and transfer unit.</span></span> 
    <span data-ttu-id="56386-168">가져오기/내보내기 수 toocopy tooa 표준 저장소 계정을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-168">Import/Export can be used toocopy tooa standard storage account.</span></span> <span data-ttu-id="56386-169">AzCopy와 같은 도구를 사용 하 여 표준 저장소 toopremium 저장소 계정에서 toocopy가 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-169">You will need toocopy from standard storage toopremium storage account using a tool like AzCopy.</span></span>


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a><span data-ttu-id="56386-170">관리 되는 만들기 hello에서 이미지에 VHD 업로드</span><span class="sxs-lookup"><span data-stu-id="56386-170">Create a managed image from hello uploaded VHD</span></span> 

<span data-ttu-id="56386-171">일반화된 OS VHD를 사용하여 관리 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56386-171">Create a managed image using your generalized OS VHD.</span></span> <span data-ttu-id="56386-172">사용자의 정보로 hello 값을 대체 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-172">Replace hello values with your own information.</span></span>


1.  <span data-ttu-id="56386-173">먼저, hello 공통 매개 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-173">First, set hello common parameters:</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  <span data-ttu-id="56386-174">일반화 된 운영 체제 VHD를 사용 하 여 hello 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56386-174">Create hello image using your generalized OS VHD.</span></span>

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="56386-175">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="56386-175">Create a virtual network</span></span>
<span data-ttu-id="56386-176">Hello vNet 및 hello의 서브넷을 만들 [가상 네트워크](../../virtual-network/virtual-networks-overview.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-176">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="56386-177">Hello 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56386-177">Create hello subnet.</span></span> <span data-ttu-id="56386-178">이 예에서는 이라는 서브넷을 만듭니다 *mySubnet* hello 주소 접두사와 *10.0.0.0/24*합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-178">This example creates a subnet named *mySubnet* with hello address prefix of *10.0.0.0/24*.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="56386-179">Hello 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56386-179">Create hello virtual network.</span></span> <span data-ttu-id="56386-180">이 예제에서는 명명 된 가상 네트워크를 만들어 *myVnet* hello 주소 접두사와 *10.0.0.0/16*합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-180">This example creates a virtual network named *myVnet* with hello address prefix of *10.0.0.0/16*.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="56386-181">공용 IP 주소 및 네트워크 인터페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="56386-181">Create a public IP address and network interface</span></span>

<span data-ttu-id="56386-182">필요한 tooenable hello 가상 네트워크의 hello 가상 컴퓨터와의 통신을는 [공용 IP 주소](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) 및 네트워크 인터페이스.</span><span class="sxs-lookup"><span data-stu-id="56386-182">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="56386-183">공용 IP 주소 만들기.</span><span class="sxs-lookup"><span data-stu-id="56386-183">Create a public IP address.</span></span> <span data-ttu-id="56386-184">이 예에서는 *myPip*라는 공용 IP 주소를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56386-184">This example creates a public IP address named *myPip*.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="56386-185">Hello NIC. 만들기</span><span class="sxs-lookup"><span data-stu-id="56386-185">Create hello NIC.</span></span> <span data-ttu-id="56386-186">이 예에서는 **myNic**라는 NIC를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56386-186">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="56386-187">Hello 네트워크 보안 그룹 및 RDP 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="56386-187">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="56386-188">toobe 수 toolog tooyour에서 RDP를 사용 하 여 VM을 toohave RDP 포트 3389에 대 한 액세스를 허용 하는 네트워크 보안 규칙 (NSG) 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-188">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="56386-189">이 예에서는 포트 3389를 통한 RDP 트래픽을 허용하는 *myRdpRule*이라는 규칙을 포함하는 *myNsg*로 명명된 NSG를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56386-189">This example creates an NSG named *myNsg* that contains a rule called *myRdpRule* that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="56386-190">Nsg에 대 한 자세한 내용은 참조 [PowerShell을 사용 하 여 Azure에서 VM 포트 tooa 여](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-190">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

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


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="56386-191">Hello 가상 네트워크에 대 한 변수 만들기</span><span class="sxs-lookup"><span data-stu-id="56386-191">Create a variable for hello virtual network</span></span>

<span data-ttu-id="56386-192">가상 네트워크를 완료 하는 hello에 대 한 변수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="56386-192">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="56386-193">Hello VM에 대 한 hello 자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="56386-193">Get hello credentials for hello VM</span></span>

<span data-ttu-id="56386-194">hello 다음 cmdlet이 열립니다 입력할 수 있는 새 사용자 이름 및 암호 toouse hello 로컬 관리자 계정으로 원격으로 hello VM에 액세스 하기 위한 창.</span><span class="sxs-lookup"><span data-stu-id="56386-194">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a><span data-ttu-id="56386-195">Hello VM 이름 및 크기 toohello VM 구성에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-195">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="56386-196">Hello에 대 한 원본 이미지로 집합 hello VM 이미지 새 VM</span><span class="sxs-lookup"><span data-stu-id="56386-196">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="56386-197">관리 되는 hello VM 이미지의 hello ID를 사용 하 여 hello 소스 이미지를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-197">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="56386-198">운영 체제 구성 hello를 설정 하 고 hello NIC. 추가</span><span class="sxs-lookup"><span data-stu-id="56386-198">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="56386-199">Hello 저장소 유형 (PremiumLRS 또는 StandardLRS)와 hello OS 디스크의 hello 크기를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-199">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="56386-200">이 예에서는 설정 hello 계정 유형 너무*PremiumLRS*, 디스크 크기를 너무 hello*128GB* 및 디스크 캐싱에 너무*ReadWrite*합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-200">This example sets hello account type too*PremiumLRS*, hello disk size too*128 GB* and disk caching too*ReadWrite*.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="56386-201">Hello VM 만들기</span><span class="sxs-lookup"><span data-stu-id="56386-201">Create hello VM</span></span>

<span data-ttu-id="56386-202">Hello hello에 저장 된 hello 구성을 사용 하 여 새 VM 만들기 **$vm** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="56386-202">Create hello new VM using hello configuration stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="56386-203">VM이 생성 되었고 해당 hello를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-203">Verify that hello VM was created</span></span>
<span data-ttu-id="56386-204">새로 만든 VM의 hello hello 나타나야 완료 되 면 [Azure 포털](https://portal.azure.com) 아래 **찾아보기** > **가상 컴퓨터**, 또는 hello 다음을 사용 하 여 PowerShell 명령:</span><span class="sxs-lookup"><span data-stu-id="56386-204">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="56386-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="56386-205">Next steps</span></span>

<span data-ttu-id="56386-206">tooyour 새 가상 컴퓨터, hello에 찾아보기 toohello VM에에서 toosign [포털](https://portal.azure.com), 클릭 **연결**, 및 열기 hello RDP 원격 데스크톱 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="56386-206">toosign in tooyour new virtual machine, browse toohello VM in hello [portal](https://portal.azure.com), click **Connect**, and open hello Remote Desktop RDP file.</span></span> <span data-ttu-id="56386-207">Tooyour 새 가상 컴퓨터에 프로그램 원래 가상 컴퓨터 toosign의 hello 계정 자격 증명을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-207">Use hello account credentials of your original virtual machine toosign in tooyour new virtual machine.</span></span> <span data-ttu-id="56386-208">자세한 내용은 참조 [어떻게 tooconnect 로그온 tooan Azure 가상 컴퓨터 및 Windows를 실행](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="56386-208">For more information, see [How tooconnect and log on tooan Azure virtual machine running Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

