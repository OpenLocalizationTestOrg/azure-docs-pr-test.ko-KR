---
title: "Azure에서 VHD로 관리 디스크 만들기 | Microsoft Docs"
description: "Resource Manager 배포 모델을 사용하여 현재 Azure 저장소 계정에 있는 VHD로 관리 디스크를 만듭니다."
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
ms.date: 02/05/2017
ms.author: cynthn
ms.openlocfilehash: c03ebf73f1090b595149daf2eb3e274b05822f4f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-managed-disks-from-unmanaged-disks-in-a-storage-account"></a><span data-ttu-id="cc33c-103">저장소 계정의 비관리 디스크로 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="cc33c-103">Create managed disks from unmanaged disks in a storage account</span></span>

<span data-ttu-id="cc33c-104">현재 Azure 저장소 계정에 있는 기존 데이터 디스크 또는 OS 디스크로 관리 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-104">A managed disk can be created from an existing data disk or an OS disk that is currently in an Azure storage account.</span></span> <span data-ttu-id="cc33c-105">또한 VM의 새 데이터 디스크로 사용할 수 있는 빈 디스크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-105">You can also create an empty disk that can be used as a new data disk for a VM.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="cc33c-106">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="cc33c-106">Before you begin</span></span>
<span data-ttu-id="cc33c-107">PowerShell을 사용하는 경우 AzureRM.Compute PowerShell 모듈이 최신 버전인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-107">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="cc33c-108">다음 명령을 실행하여 PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-108">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="cc33c-109">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="cc33c-109">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>


## <a name="create-a-managed-disk-from-a-vhd-in-an-azure-storage-account"></a><span data-ttu-id="cc33c-110">Azure 저장소 계정에서 VHD로 관리 디스크 만들기 | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="cc33c-110">Create a managed disk from a VHD in an Azure storage account</span></span>

<span data-ttu-id="cc33c-111">이 예제에서는 VHD의 디스크로 관리 디스크를 만들고 나중에 사용할 수 있도록 **$disk1** 매개 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-111">In the example we create a disk from a VHD as managed disk and assign it to the parameter **$disk1** to use later.</span></span> 

<span data-ttu-id="cc33c-112">관리 디스크는 **미국 서부** 위치의 **myResourceGroup**이라는 리소스 그룹에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-112">The managed disk will be created in the **West-US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="cc33c-113">디스크 이름은 **myDisk**로 할 것이며 이전에 **mystorageaccount**라는 저장소 계정에 업로드한 **myDisk.vhd** VHD 파일로 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-113">The disk will be named **myDisk** and it will be created from a VHD file named **myDisk.vhd** we previously uploaded to a storage account named **mystorageaccount**.</span></span> <span data-ttu-id="cc33c-114">관리 디스크는 프리미엄 LRS(로컬 중복 저장소)에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-114">The managed disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="cc33c-115">StandardLRS 및 PremiumLRS는 관리 디스크에 제공되는 유일한 **-AccountType** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-115">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span> 

1.  <span data-ttu-id="cc33c-116">일부 매개 변수 설정</span><span class="sxs-lookup"><span data-stu-id="cc33c-116">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $diskName = "myDisk"
    $vhdUri = "https://mystorageaccount.blob.core.windows.net/vhds/myDisk.vhd"
    ```

2. <span data-ttu-id="cc33c-117">데이터 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-117">Create the data disk.</span></span> 
    ```powershell
    $disk1 = New-AzureRmDisk -DiskName $diskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Import -SourceUri $vhdUri) -ResourceGroupName $rgName
    ```
    
    

## <a name="create-an-empty-data-disk-as-a-managed-disk"></a><span data-ttu-id="cc33c-118">관리 디스크로 빈 데이터 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="cc33c-118">Create an empty data disk as a managed disk</span></span>

<span data-ttu-id="cc33c-119">이 예제에서는 관리 디스크로 빈 데이터 디스크를 만들고 나중에 사용할 수 있도록 **$dataDisk2** 매개 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-119">In the example we create an empty data disk as managed disk and assign it to the parameter **$dataDisk2** to use later.</span></span> <span data-ttu-id="cc33c-120">실행 중인 VM에 빈 데이터 디스크가 연결되면 diskmgmt.msc를 사용하거나 [원격으로 WinRM 및 스크립트를 사용](attach-disk-ps.md#initialize-the-disk)하여 빈 데이터 디스크를 초기화하고 VM에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-120">An empty data disk will need to be initialized logging in to the VM and using diskmgmt.msc or [remotely using WinRM and a script](attach-disk-ps.md#initialize-the-disk), once it is attached to a running VM.</span></span>

<span data-ttu-id="cc33c-121">빈 데이터 디스크는 **미국 중서부** 위치의 **myResourceGroup** 리소스 그룹에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-121">The empty data disk will be created in the **West Central US** location, in a resource group named **myResourceGroup**.</span></span> <span data-ttu-id="cc33c-122">디스크 이름은 **myEmptyDataDisk**입니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-122">The disk will be named **myEmptyDataDisk**.</span></span> <span data-ttu-id="cc33c-123">빈 디스크는 프리미엄 LRS(로컬 중복 저장소)에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-123">The empty disk will be created in premium locally-redundant storage (LRS).</span></span> <span data-ttu-id="cc33c-124">StandardLRS 및 PremiumLRS는 관리 디스크에 제공되는 유일한 **-AccountType** 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-124">StandardLRS and PremiumLRS are the only **-AccountType** options available for managed disks.</span></span>

<span data-ttu-id="cc33c-125">이 예제의 디스크 크기는 128GB입니다. 하지만 VM에서 실행 중인 모든 응용 프로그램의 요구를 충족하는 크기를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-125">The disk size in this example is 128GB, but you should choose a size that meets the needs of any applications running on your VM.</span></span>

1.  <span data-ttu-id="cc33c-126">일부 매개 변수 설정</span><span class="sxs-lookup"><span data-stu-id="cc33c-126">Set some parameters</span></span>

    ```powershell
    $rgName = "myResourceGroup"
    $location = "West Central US"
    $dataDiskName = "myEmptyDataDisk"
    ```

2. <span data-ttu-id="cc33c-127">데이터 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-127">Create the data disk.</span></span>
    ```powershell
    $dataDisk2 = New-AzureRmDisk -DiskName $dataDiskName -Disk (New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128) -ResourceGroupName $rgName
    ```
    
## <a name="next-steps"></a><span data-ttu-id="cc33c-128">다음 단계</span><span class="sxs-lookup"><span data-stu-id="cc33c-128">Next Steps</span></span>   
- <span data-ttu-id="cc33c-129">이미 VM이 있는 경우 [데이터 디스크를 연결](attach-disk-portal.md)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cc33c-129">If you already have a VM, you can [attach a data disk](attach-disk-portal.md).</span></span>
