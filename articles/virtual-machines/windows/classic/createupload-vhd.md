---
title: "Powershell을 사용하여 VM 이미지 만들기 및 업로드 | Microsoft Docs"
description: "클래식 배포 모델 및 Azure Powershell을 사용하여 일반화된 Windows Server 이미지(VHD)를 만들고 업로드하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: bc75c8cdd98b0ea0fbff6483c0e3c9d4468d3941
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-windows-server-vhd-to-azure"></a><span data-ttu-id="8e88d-103">Windows Server VHD를 만들어서 Azure에 업로드</span><span class="sxs-lookup"><span data-stu-id="8e88d-103">Create and upload a Windows Server VHD to Azure</span></span>
<span data-ttu-id="8e88d-104">이 문서에서는 일반화된 자체 VM 이미지를 VHD(가상 하드 디스크)로 업로드하고 이를 가상 컴퓨터를 만드는 데 사용하는 방법을 소개합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-104">This article shows you how to upload your own generalized VM image as a virtual hard disk (VHD) so you can use it to create virtual machines.</span></span> <span data-ttu-id="8e88d-105">Microsoft Azure의 디스크 및 VHD에 대한 자세한 내용은 [가상 컴퓨터용 디스크 및 VHD에 대하여](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e88d-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8e88d-106">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8e88d-107">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="8e88d-108">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="8e88d-109">Resource Manager 모델을 사용하여 가상 컴퓨터를 [업로드](../upload-generalized-managed.md)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using the Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8e88d-110">필수 조건</span><span class="sxs-lookup"><span data-stu-id="8e88d-110">Prerequisites</span></span>
<span data-ttu-id="8e88d-111">이 문서에서는 사용자가 다음 작업을 수행한 것으로 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-111">This article assumes you have:</span></span>

* <span data-ttu-id="8e88d-112">**Azure 구독** - 계정이 없는 경우 [무료로 Azure 계정을 개설할 수 있습니다](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="8e88d-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="8e88d-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - Microsoft Azure PowerShell 모듈이 설치되고 구독을 사용하도록 구성되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have the Microsoft Azure PowerShell module installed and configured to use your subscription.</span></span>
* <span data-ttu-id="8e88d-114">**.VHD 파일** - .vhd 파일에 저장되고 가상 컴퓨터에 연결된 지원되는 Windows 운영 체제</span><span class="sxs-lookup"><span data-stu-id="8e88d-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached to a virtual machine.</span></span> <span data-ttu-id="8e88d-115">VHD에서 실행 중인 서버 역할이 Sysprep에서 지원되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-115">Check to see if the server roles running on the VHD are supported by Sysprep.</span></span> <span data-ttu-id="8e88d-116">자세한 내용은 [서버 역할에 대한 Sysprep 지원](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e88d-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8e88d-117">VHDX 형식은 Microsoft Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-117">The VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="8e88d-118">Hyper-V 관리자 또는 [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx)을 사용하여 디스크를 VHD 형식으로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-118">You can convert the disk to VHD format using Hyper-V Manager or the [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="8e88d-119">자세한 내용은 이 [블로그 게시물](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e88d-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-the-vhd"></a><span data-ttu-id="8e88d-120">1 단계: VHD 준비</span><span class="sxs-lookup"><span data-stu-id="8e88d-120">Step 1: Prep the VHD</span></span>
<span data-ttu-id="8e88d-121">Azure에 VHD를 업로드하기 전에 Sysprep 도구를 사용하여 일반화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-121">Before you upload the VHD to Azure, it needs to be generalized by using the Sysprep tool.</span></span> <span data-ttu-id="8e88d-122">그러면 VHD가 이미지로 사용하도록 준비됩니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-122">This prepares the VHD to be used as an image.</span></span> <span data-ttu-id="8e88d-123">Sysprep에 대한 자세한 내용은 [Sysprep 사용 방법: 소개](http://technet.microsoft.com/library/bb457073.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8e88d-123">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="8e88d-124">Sysprep를 실행하기 전에 VM을 백업합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-124">Back up the VM before running Sysprep.</span></span>

<span data-ttu-id="8e88d-125">운영 체제를 설치한 가상 컴퓨터에서 다음 절차를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-125">From the virtual machine that the operating system was installed to, complete the following procedure:</span></span>

1. <span data-ttu-id="8e88d-126">운영 체제에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-126">Sign in to the operating system.</span></span>
2. <span data-ttu-id="8e88d-127">관리자로 명령 프롬프트 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="8e88d-128">디렉터리를 **%windir%\system32\sysprep**로 변경한 후 `sysprep.exe`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-128">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![명령 프롬프트 창 열기](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="8e88d-130">**시스템 준비 도구** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-130">The **System Preparation Tool** dialog box appears.</span></span>

   ![Sysprep 시작](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="8e88d-132">**시스템 준비 도구**에서 **시스템 OOBE(첫 실행 경험) 입력**을 선택하고 **일반화**를 선택했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-132">In the **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="8e88d-133">**종료 옵션**에서 **종료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="8e88d-134">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="8e88d-135">2단계: 저장소 계정 및 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="8e88d-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="8e88d-136">.vhd 파일을 업로드할 장소가 있도록 Azure에 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-136">You need a storage account in Azure so you have a place to upload the .vhd file.</span></span> <span data-ttu-id="8e88d-137">이 단계는 계정을 만들거나 기존 계정에서 필요한 정보를 가져오는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-137">This step shows you how to create an account, or get the info you need from an existing account.</span></span> <span data-ttu-id="8e88d-138">&lsaquo; 대괄호 &rsaquo;의 변수 값을 사용자의 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-138">Replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="8e88d-139">로그인</span><span class="sxs-lookup"><span data-stu-id="8e88d-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="8e88d-140">Azure 구독을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="8e88d-141">새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-141">Create a new storage account.</span></span> <span data-ttu-id="8e88d-142">저장소 계정의 이름은 고유한 3-24자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-142">The name of the storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="8e88d-143">이름은 문자와 숫자의 조합으로 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-143">The name can be any combination of letters and numbers.</span></span> <span data-ttu-id="8e88d-144">"미국 동부"와 같은 위치도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-144">You also need to specify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="8e88d-145">새 저장소 계정을 기본값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-145">Set the new storage account as the default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="8e88d-146">새 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-the-vhd-file"></a><span data-ttu-id="8e88d-147">3단계: .vhd 파일 업로드</span><span class="sxs-lookup"><span data-stu-id="8e88d-147">Step 3: Upload the .vhd file</span></span>
<span data-ttu-id="8e88d-148">[Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) 를 사용하여 VHD를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-148">Use the [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) to upload the VHD.</span></span>

<span data-ttu-id="8e88d-149">이전 단계에서 사용한 Azure PowerShell 창에서 다음 명령을 입력하고 &lsaquo; brackets &rsaquo;의 변수를 자체 정보로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-149">From the Azure PowerShell window you used in the previous step, type the following command and replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-the-image-to-your-list-of-custom-images"></a><span data-ttu-id="8e88d-150">4단계: 사용자 지정 이미지 목록에 이미지 추가</span><span class="sxs-lookup"><span data-stu-id="8e88d-150">Step 4: Add the image to your list of custom images</span></span>
<span data-ttu-id="8e88d-151">[Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet을 사용하여 사용자 지정 이미지 목록에 이미지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-151">Use the [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet to add the image to the list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="8e88d-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8e88d-152">Next steps</span></span>
<span data-ttu-id="8e88d-153">이제 업로드한 이미지를 사용하여 [사용자 지정 VM을 만들](createportal.md) 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8e88d-153">You can now [create a custom VM](createportal.md) using the image you uploaded.</span></span>
