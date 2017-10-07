---
title: "백업에 대 한 Azure 관리 되는 디스크의 복사본 aaaCreate | Microsoft Docs"
description: "위쪽 또는 문제 해결을 다시 디스크는 Azure 관리 되는 디스크 toouse의 복사본을 발급 하는 toocreate 방법에 대해 알아봅니다."
documentationcenter: 
author: cwatson-cat
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 15eb778e-fc07-45ef-bdc8-9090193a6d20
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 2/9/2017
ms.author: cwatson
ms.openlocfilehash: 2f33dbbee624bcd813f3c7c3e3401072d0933714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-copy-of-a-vhd-stored-as-an-azure-managed-disk-by-using-managed-snapshots"></a><span data-ttu-id="e4fe0-103">관리 스냅숏을 사용하여 Azure Managed Disk로 저장된 VHD 복사본 만들기</span><span class="sxs-lookup"><span data-stu-id="e4fe0-103">Create a copy of a VHD stored as an Azure Managed Disk by using Managed Snapshots</span></span>
<span data-ttu-id="e4fe0-104">백업에 대 한 관리 되는 디스크의 스냅숏을 또는 hello 스냅숏에서 관리 되는 디스크를 만들어 tooa 테스트 가상 컴퓨터 tootroubleshoot를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-104">Take a snapshot of a Managed Disk for backup or create a Managed Disk from hello snapshot and attach it tooa test virtual machine tootroubleshoot.</span></span> <span data-ttu-id="e4fe0-105">관리 스냅숏은 VM Managed Disk의 특정 시점 전체 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-105">A Managed Snapshot is a full point-in-time copy of a VM Managed Disk.</span></span> <span data-ttu-id="e4fe0-106">VHD의 읽기 전용 복사본을 만들어서 기본적으로 표준 Managed Disk로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-106">It creates a read-only copy of your VHD and, by default, stores it as a Standard Managed Disk.</span></span> <span data-ttu-id="e4fe0-107">Managed Disk에 대한 자세한 내용은 [Azure Managed Disks 개요](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-107">For more information about Managed Disks, see [Azure Managed Disks overview](managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>

<span data-ttu-id="e4fe0-108">가격 책정에 대한 자세한 내용은 [Azure Storage 가격 책정](https://azure.microsoft.com/pricing/details/managed-disks/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-108">For information about pricing, see [Azure Storage Pricing](https://azure.microsoft.com/pricing/details/managed-disks/).</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="e4fe0-109">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="e4fe0-109">Before you begin</span></span>
<span data-ttu-id="e4fe0-110">PowerShell을 사용 하는 경우 hello hello AzureRM.Compute PowerShell 모듈의 최신 버전이 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-110">If you use PowerShell, make sure that you have hello latest version of hello AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="e4fe0-111">실행 명령 tooinstall 다음 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-111">Run hello following command tooinstall it.</span></span>

```
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="e4fe0-112">자세한 내용은 [Azure PowerShell 버전 관리](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-112">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>

## <a name="copy-hello-vhd-with-a-snapshot"></a><span data-ttu-id="e4fe0-113">스냅숏 사용 하 여 hello VHD 복사</span><span class="sxs-lookup"><span data-stu-id="e4fe0-113">Copy hello VHD with a snapshot</span></span>
<span data-ttu-id="e4fe0-114">Hello Azure 포털 또는 PowerShell tootake hello 관리 되는 디스크의 스냅숏 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-114">Use either hello Azure portal or PowerShell tootake a snapshot of hello Managed Disk.</span></span>

### <a name="use-azure-portal-tootake-a-snapshot"></a><span data-ttu-id="e4fe0-115">Azure 포털 tootake 스냅숏을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e4fe0-115">Use Azure portal tootake a snapshot</span></span> 

1. <span data-ttu-id="e4fe0-116">Toohello 로그인 [Azure 포털](https://portal.azure.com)합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-116">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e4fe0-117">왼쪽 위에서 hello 년부터 클릭 **새로** 검색 한 **스냅숏**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-117">Starting in hello upper left, click **New** and search for **snapshot**.</span></span>
3. <span data-ttu-id="e4fe0-118">Hello 스냅숏 블레이드에서 클릭 **만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-118">In hello Snapshot blade, click **Create**.</span></span>
4. <span data-ttu-id="e4fe0-119">입력 한 **이름** hello 스냅숏에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-119">Enter a **Name** for hello snapshot.</span></span>
5. <span data-ttu-id="e4fe0-120">기존 선택 [리소스 그룹](../../azure-resource-manager/resource-group-overview.md#resource-groups) 또는 새 유형 hello 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-120">Select an existing [Resource group](../../azure-resource-manager/resource-group-overview.md#resource-groups) or type hello name for a new one.</span></span> 
6. <span data-ttu-id="e4fe0-121">Azure 데이터 센터 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-121">Select an Azure datacenter Location.</span></span>  
7. <span data-ttu-id="e4fe0-122">에 대 한 **원본 디스크**, 선택 hello toosnapshot 디스크 관리.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-122">For **Source disk**, select hello Managed Disk toosnapshot.</span></span>
8. <span data-ttu-id="e4fe0-123">선택 hello **계정 유형** toouse toostore hello 스냅숏 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-123">Select hello **Account type** toouse toostore hello snapshot.</span></span> <span data-ttu-id="e4fe0-124">고성능 디스크에 저장할 필요가 없다면 **Standard_LRS**를 권장합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-124">We recommend **Standard_LRS** unless you need it stored on a high performing disk.</span></span>
9. <span data-ttu-id="e4fe0-125">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-125">Click **Create**.</span></span>

### <a name="use-powershell-tootake-a-snapshot"></a><span data-ttu-id="e4fe0-126">PowerShell tootake 스냅숏을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="e4fe0-126">Use PowerShell tootake a snapshot</span></span>
<span data-ttu-id="e4fe0-127">hello 다음 단계 tooget hello VHD 복사 toobe 디스크 하는 방법을 알려주는 hello 스냅숏 구성을 만들고 새로 AzureRmSnapshot hello cmdlet을 사용 하 여 hello 디스크의 스냅숏을<!--Add link toocmdlet when available-->합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-127">hello following steps show you how tooget hello VHD disk toobe copied, create hello snapshot configurations, and take a snapshot of hello disk by using hello New-AzureRmSnapshot cmdlet<!--Add link toocmdlet when available-->.</span></span> 

1. <span data-ttu-id="e4fe0-128">일부 매개 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-128">Set some parameters.</span></span> 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'southeastasia' 
$dataDiskName = 'ContosoMD_datadisk1' 
$snapshotName = 'ContosoMD_datadisk1_snapshot1'  
```
  <span data-ttu-id="e4fe0-129">Hello 매개 변수 값을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-129">Replace hello parameter values:</span></span>
  -  <span data-ttu-id="e4fe0-130">"myResourceGroup" hello VM의 리소스 그룹을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-130">"myResourceGroup" with hello VM's resource group.</span></span>
  -  <span data-ttu-id="e4fe0-131">"southeastasia" hello 지리적 위치에 저장 된 관리 되는 스냅숏을 저장할와 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-131">"southeastasia" with hello geographic location where you want your Managed Snapshot stored.</span></span> <!---How do you look these up? -->
  -  <span data-ttu-id="e4fe0-132">"ContosoMD_datadisk1" hello 이름의 hello VHD 디스크 toocopy 되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-132">"ContosoMD_datadisk1" with hello name of hello VHD disk that you want toocopy.</span></span>
  -  <span data-ttu-id="e4fe0-133">"ContosoMD_datadisk1_snapshot1" hello로 이름을 지정 하면 새 스냅숏을 hello에 대 한 toouse 원하는 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-133">"ContosoMD_datadisk1_snapshot1" with hello name you want toouse for hello new snapshot.</span></span>

2. <span data-ttu-id="e4fe0-134">Hello VHD 디스크 toobe를 복사를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-134">Get hello VHD disk toobe copied.</span></span>

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $dataDiskName 
```
3. <span data-ttu-id="e4fe0-135">Hello 스냅숏 구성을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-135">Create hello snapshot configurations.</span></span> 

 ```powershell
$snapshot =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -CreateOption Copy -Location $location 
```
4. <span data-ttu-id="e4fe0-136">Hello 스냅숏을 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-136">Take hello snapshot.</span></span>

 ```powershell
New-AzureRmSnapshot -Snapshot $snapshot -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName 
```
<span data-ttu-id="e4fe0-137">Hello 매개 변수를 사용 하 여 관리 되는 디스크 toouse hello 스냅숏 toocreate를 계획 하 고 toobe 높은 수행 해야 하는 VM을 연결 하는 경우 `-AccountType Premium_LRS` hello AzureRmSnapshot 새로 만들기 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-137">If you plan toouse hello snapshot toocreate a Managed Disk and attach it a VM that needs toobe high performing, use hello parameter `-AccountType Premium_LRS` with hello New-AzureRmSnapshot command.</span></span> <span data-ttu-id="e4fe0-138">hello 매개 변수 hello 스냅숏을 생성 되어 프리미엄 관리 되는 디스크로 저장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-138">hello parameter creates hello snapshot so that it's stored as a Premium Managed Disk.</span></span> <span data-ttu-id="e4fe0-139">프리미엄 Managed Disks는 표준 Managed Disks보다 비용이 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-139">Premium Managed Disks are more expensive than Standard.</span></span> <span data-ttu-id="e4fe0-140">따라서 해당 매개 변수를 사용하기 전에 프리미엄이 필요한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e4fe0-140">So be sure you really need Premium before using that parameter.</span></span>


