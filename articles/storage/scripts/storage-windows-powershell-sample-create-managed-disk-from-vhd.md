---
title: "PowerShell 스크립트 샘플-aaaAzure 동일 하거나 다른 구독에서 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만들 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 동일한 또는 다른 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="23c41-103">PowerShell을 사용하여 동일한 또는 다른 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="23c41-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="23c41-104">이 스크립트는 같은 구독 또는 다른 구독의 저장소 계정에 VHD 파일의 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="23c41-105">이 스크립트 tooimport는 특수화 된 (하지 일반화/sysprepped) VHD toomanaged OS 디스크 toocreate 가상 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="23c41-106">또한 tooimport 데이터 VHD toomanaged 데이터 디스크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="23c41-107">VHD 파일에서 단시간에 동일한 관리 디스크를 여러 개 만들지 마세요.</span><span class="sxs-lookup"><span data-stu-id="23c41-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="23c41-108">toocreate 디스크 vhd 파일에서 관리 되는, hello vhd 파일의 blob 스냅숏이 생성 및 관리 되는 사용 되는 toocreate 디스크 됩니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="23c41-109">하나의 blob 스냅숏을 만들지 못했습니다. 디스크는 1 분에서 만들 수 있습니다 due toothrottling 합니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="23c41-110">tooavoid 이러한 조절은 만들기는 [hello vhd 파일에서 관리 되는 스냅숏](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) 하 고 사용 하 여 hello 관리 됩니다 스냅숏 toocreate 여러 관리 되는 디스크 짧은 시간 내에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="23c41-111">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="23c41-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="23c41-112">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="23c41-112">Script explanation</span></span>

<span data-ttu-id="23c41-113">이 스크립트 명령 toocreate 다음 다른 구독에는 VHD에서 관리 되는 디스크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="23c41-114">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="23c41-115">명령</span><span class="sxs-lookup"><span data-stu-id="23c41-115">Command</span></span> | <span data-ttu-id="23c41-116">참고 사항</span><span class="sxs-lookup"><span data-stu-id="23c41-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="23c41-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="23c41-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="23c41-118">디스크 만들기에 사용되는 디스크 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="23c41-119">저장소 유형, 위치, 리소스 Id의 hello 저장소 계정 hello 부모 VHD 저장 된 VHD hello 부모의 VHD URI를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="23c41-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="23c41-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="23c41-121">매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="23c41-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="23c41-122">Next steps</span></span>

[<span data-ttu-id="23c41-123">관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="23c41-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="23c41-124">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="23c41-125">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="23c41-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
