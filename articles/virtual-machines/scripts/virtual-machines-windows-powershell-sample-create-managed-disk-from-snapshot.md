---
title: "PowerShell 스크립트 샘플-aaaAzure 스냅숏으로에서 관리 되는 디스크를 만들 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 스냅숏에서 관리 디스크 만들기"
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
ms.openlocfilehash: b99413b4c3e9a662a5fef74b7e4aeb5ecbb26af4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="1e693-103">PowerShell을 사용하여 스냅숏에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="1e693-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="1e693-104">이 스크립트는 스냅숏에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="1e693-105">OS 및 데이터 디스크의 스냅숏 기반에서으로 가상 컴퓨터 toorestore 방법을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="1e693-106">각 스냅숏에서 OS 및 데이터 관리 디스크를 만든 다음 관리 디스크를 연결하여 새 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="1e693-107">스냅숏에서 만든 데이터 디스크를 연결하여 기존 VM의 데이터 디스크를 복원할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="1e693-108">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="1e693-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="1e693-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="1e693-109">Script explanation</span></span>

<span data-ttu-id="1e693-110">이 스크립트 명령 toocreate 다음 스냅숏에서 관리 되는 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="1e693-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="1e693-112">명령</span><span class="sxs-lookup"><span data-stu-id="1e693-112">Command</span></span> | <span data-ttu-id="1e693-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="1e693-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1e693-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="1e693-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="1e693-115">스냅숏 속성을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="1e693-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="1e693-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="1e693-117">디스크 만들기에 사용되는 디스크 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="1e693-118">Hello 리소스 부모 스냅숏과 hello 저장소 유형의 hello 위치 같습니다 위치 hello 부모 스냅숏의 Id를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="1e693-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="1e693-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="1e693-120">매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="1e693-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1e693-121">Next steps</span></span>

[<span data-ttu-id="1e693-122">관리 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="1e693-122">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="1e693-123">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="1e693-124">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="1e693-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
