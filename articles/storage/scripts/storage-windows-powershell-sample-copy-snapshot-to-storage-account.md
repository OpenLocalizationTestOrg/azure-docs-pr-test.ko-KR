---
title: "Azure PowerShell 스크립트 샘플 - 다른 지역의 저장소 계정으로 스냅숏을 VHD로 내보내기/복사 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 다른 지역의 저장소 계정으로 스냅숏을 VHD로 내보내기/복사"
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
ms.openlocfilehash: 80f83f4b66165ddd2bdd0edca2be5d026cb11a9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="8f381-103">PowerShell을 사용하여 다른 지역의 저장소 계정으로 관리 스냅숏을 VHD로 내보내기/복사</span><span class="sxs-lookup"><span data-stu-id="8f381-103">Export/Copy managed snapshots as VHD to a storage account in different region with PowerShell</span></span>

<span data-ttu-id="8f381-104">이 스크립트는 다른 지역의 저장소 계정으로 관리 스냅숏을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="8f381-105">먼저 스냅숏의 SAS URI를 생성한 다음 이를 사용하여 다른 지역의 저장소 계정으로 스냅숏을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="8f381-106">이 스크립트를 사용하여 재해 복구를 위해 다른 지역에서 관리 디스크의 백업을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8f381-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="8f381-107">Sample script</span></span>

<span data-ttu-id="8f381-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "스냅숏 복사")]</span><span class="sxs-lookup"><span data-stu-id="8f381-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="8f381-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="8f381-109">Script explanation</span></span>

<span data-ttu-id="8f381-110">이 스크립트에서는 다음 명령을 사용하여 관리 스냅숏의 SAS URI를 생성하고 SAS URI를 사용하여 저장소 계정에 스냅숏을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="8f381-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8f381-112">명령</span><span class="sxs-lookup"><span data-stu-id="8f381-112">Command</span></span> | <span data-ttu-id="8f381-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="8f381-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8f381-114">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="8f381-114">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="8f381-115">저장소 계정에 스냅숏을 복사하는 데 사용되는 스냅숏의 SAS URI를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-115">Generates SAS URI for a snapshot that is used to copy it to a storage account.</span></span> |
| [<span data-ttu-id="8f381-116">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="8f381-116">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="8f381-117">계정 이름과 키를 사용하여 저장소 계정 컨텍스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-117">Creates a storage account context using the account name and key.</span></span> <span data-ttu-id="8f381-118">이 컨텍스트는 저장소 계정에 대한 읽기/쓰기 작업을 수행하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-118">This context can be used to perform read/write operations on the storage account.</span></span> |
| [<span data-ttu-id="8f381-119">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="8f381-119">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="8f381-120">스냅숏의 기본 VHD를 저장소 계정에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-120">Copies the underlying VHD of a snapshot to a storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8f381-121">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8f381-121">Next steps</span></span>

[<span data-ttu-id="8f381-122">VHD에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="8f381-122">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="8f381-123">관리 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="8f381-123">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="8f381-124">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f381-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8f381-125">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f381-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>