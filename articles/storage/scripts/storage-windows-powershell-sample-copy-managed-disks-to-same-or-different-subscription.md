---
title: "PowerShell 스크립트 샘플-aaaAzure 복사 (이동) 관리 되는 디스크 toosame 또는 다른 구독 | Microsoft Docs"
description: "Azure PowerShell 스크립트 샘플-복사 (이동) 관리 되는 디스크 toosame 또는 다른 구독"
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
ms.openlocfilehash: 5a92118e10a14615e5b1713f1b90188b37b05305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="2c7a1-103">관리 되는 복사본에에서 디스크를 hello 동일 구독 또는 PowerShell과 함께 다른 구독</span><span class="sxs-lookup"><span data-stu-id="2c7a1-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="2c7a1-104">이 스크립트는 hello에 기존의 관리 되는 디스크의 복사본을 만듭니다 동일한 구독 또는 다른 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7a1-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="2c7a1-105">hello 디스크가 새로 만들어집니다 hello에 동일 지역 hello 부모 디스크를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7a1-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2c7a1-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2c7a1-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="2c7a1-107">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="2c7a1-107">Script explanation</span></span>

<span data-ttu-id="2c7a1-108">이 스크립트를 사용 하 여 다음 명령을 toocreate 사용 하 여 hello 대상 구독에 관리 되는 새 디스크를 hello hello 원본의 Id 디스크를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7a1-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="2c7a1-109">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7a1-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2c7a1-110">명령</span><span class="sxs-lookup"><span data-stu-id="2c7a1-110">Command</span></span> | <span data-ttu-id="2c7a1-111">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2c7a1-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2c7a1-112">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="2c7a1-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="2c7a1-113">디스크 만들기에 사용되는 디스크 구성을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c7a1-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="2c7a1-114">Hello 리소스 Id hello 부모 디스크와 부모 디스크의 hello 위치과 같은 위치를 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7a1-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="2c7a1-115">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="2c7a1-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="2c7a1-116">매개 변수로 전달된 디스크 구성, 디스크 이름 및 리소스 그룹 이름을 사용하여 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2c7a1-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="2c7a1-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2c7a1-117">Next steps</span></span>

[<span data-ttu-id="2c7a1-118">관리 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="2c7a1-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="2c7a1-119">Hello Azure PowerShell 모듈에 대 한 자세한 내용은 참조 하십시오. [Azure PowerShell 설명서](/powershell/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7a1-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2c7a1-120">가상 컴퓨터가 추가 PowerShell 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="2c7a1-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
