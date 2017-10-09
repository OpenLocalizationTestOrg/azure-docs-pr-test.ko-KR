---
title: "PowerShell 스크립트 샘플-관리 되는 디스크 toosame 또는 다른 구독 복사 (이동) 스냅숏 aaaAzure | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-관리 되는 디스크 toosame 또는 다른 구독 복사 (이동) 스냅숏"
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
ms.openlocfilehash: d7b8a71cc09d1950271f472e89b95bb551323be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="57afe-103">PowerShell을 사용하여 같은 구독 또는 다른 구독에 관리 디스크의 스냅숏 복사</span><span class="sxs-lookup"><span data-stu-id="57afe-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="57afe-104">이 스크립트는 hello에는 스냅숏의 복사본을 만듭니다 같은 동일한 구독 또는 다른 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="57afe-105">데이터 보관을 위해이 스크립트 toomove 스냅숏 toodifferent 구독을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="57afe-106">다른 구독에 스냅숏을 저장하여 기본 구독에서 스냅숏을 실수로 삭제하지 않도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="57afe-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="57afe-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="57afe-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="57afe-108">Script explanation</span></span>

<span data-ttu-id="57afe-109">이 스크립트 명령 toocreate 다음 사용 하 여 사용 하 여 hello 대상 구독에서 스냅숏 hello hello 소스 스냅숏의 Id입니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="57afe-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="57afe-111">명령</span><span class="sxs-lookup"><span data-stu-id="57afe-111">Command</span></span> | <span data-ttu-id="57afe-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="57afe-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="57afe-113">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="57afe-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="57afe-114">스냅숏 생성에 사용되는 스냅숏 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="57afe-115">Hello 리소스 hello 부모 스냅숏과 hello 부모 스냅숏의과 같은 위치 Id를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="57afe-116">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="57afe-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="57afe-117">매개 변수로 전달된 스냅숏 구성, 스냅숏 이름 및 리소스 그룹 이름을 사용하여 스냅숏을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="57afe-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="57afe-118">Next steps</span></span>

[<span data-ttu-id="57afe-119">스냅숏에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="57afe-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="57afe-120">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="57afe-121">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="57afe-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
