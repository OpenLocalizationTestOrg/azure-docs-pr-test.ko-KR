---
title: "Azure PowerShell 스크립트 샘플 - 관리 디스크의 스냅숏을 동일한 구독이나 다른 구독으로 복사(이동) | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플 - 관리 디스크의 스냅숏을 동일한 구독이나 다른 구독으로 복사(이동)"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 69b9b4ed86117f7fe561e7e70227e60e6a9d858e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="8666e-103">PowerShell을 사용하여 같은 구독 또는 다른 구독에 관리 디스크의 스냅숏 복사</span><span class="sxs-lookup"><span data-stu-id="8666e-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="8666e-104">이 스크립트는 같은 구독 또는 다른 구독에 스냅숏 복사본을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8666e-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="8666e-105">이 스크립트를 사용하여 데이터 보존을 위해 스냅숏을 다른 구독으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8666e-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="8666e-106">다른 구독에 스냅숏을 저장하여 기본 구독에서 스냅숏을 실수로 삭제하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="8666e-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8666e-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="8666e-107">Sample script</span></span>

<span data-ttu-id="8666e-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "스냅숏 복사")]</span><span class="sxs-lookup"><span data-stu-id="8666e-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="8666e-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="8666e-109">Script explanation</span></span>

<span data-ttu-id="8666e-110">이 스크립트에서는 다음 명령을 사용하여 원본 스냅숏의 ID를 사용하여 대상 구독에 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8666e-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="8666e-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="8666e-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="8666e-112">명령</span><span class="sxs-lookup"><span data-stu-id="8666e-112">Command</span></span> | <span data-ttu-id="8666e-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="8666e-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8666e-114">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="8666e-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="8666e-115">스냅숏 생성에 사용되는 스냅숏 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8666e-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="8666e-116">부모 스냅숏의 리소스 ID와 부모 스냅숏과 같은 위치를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8666e-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="8666e-117">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="8666e-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="8666e-118">매개 변수로 전달된 스냅숏 구성, 스냅숏 이름 및 리소스 그룹 이름을 사용하여 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8666e-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="8666e-119">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8666e-119">Next steps</span></span>

[<span data-ttu-id="8666e-120">스냅숏에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="8666e-120">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="8666e-121">Azure PowerShell 모듈에 대한 자세한 내용은 [Azure PowerShell 설명서](/powershell/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8666e-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8666e-122">추가 가상 컴퓨터 PowerShell 스크립트 샘플은 [Azure Windows VM 설명서](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8666e-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>