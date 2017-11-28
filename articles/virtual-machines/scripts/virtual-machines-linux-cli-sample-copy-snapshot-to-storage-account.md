---
title: "Azure CLI 스크립트 샘플 - 스냅숏을 VHD로 다른 지역의 저장소 계정으로 내보내기/복사 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 스냅숏을 VHD로 동일한 구독 또는 다른 구독의 저장소 계정으로 내보내기/복사"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: a6ea65aba91641ece415db4df6ae9c17b42a0954
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a><span data-ttu-id="87f36-103">CLI를 사용하여 관리 스냅숏을 VHD로 다른 지역의 저장소 계정으로 내보내기/복사</span><span class="sxs-lookup"><span data-stu-id="87f36-103">Export/Copy managed snapshots as VHD to a storage account in different region with CLI</span></span>

<span data-ttu-id="87f36-104">이 스크립트는 관리 스냅숏을 다른 지역의 저장소 계정으로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="87f36-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="87f36-105">먼저 스냅숏의 SAS URI를 생성한 다음 이를 사용하여 다른 지역의 저장소 계정으로 스냅숏을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="87f36-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="87f36-106">이 스크립트를 사용하여 재해 복구를 위해 다른 지역에서 관리 디스크의 백업을 유지 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="87f36-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="87f36-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="87f36-107">Sample script</span></span>

<span data-ttu-id="87f36-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "스냅숏 복사")]</span><span class="sxs-lookup"><span data-stu-id="87f36-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="87f36-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="87f36-109">Script explanation</span></span>

<span data-ttu-id="87f36-110">이 스크립트에서는 다음 명령을 사용하여 관리 스냅숏의 SAS URI를 생성하고 SAS URI를 사용하여 저장소 계정에 스냅숏을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="87f36-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="87f36-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="87f36-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="87f36-112">명령</span><span class="sxs-lookup"><span data-stu-id="87f36-112">Command</span></span> | <span data-ttu-id="87f36-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="87f36-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="87f36-114">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="87f36-114">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="87f36-115">기본 VHD 파일을 저장소 계정으로 복사하거나 온-프레미스로 다운로드하는 데 사용되는 읽기 전용 SAS를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="87f36-115">Generates read-only SAS that is used to copy underlying VHD file to a storage account or download it to on-premises</span></span>  |
| [<span data-ttu-id="87f36-116">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="87f36-116">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="87f36-117">하나의 저장소 계정에서 다른 저장소 계정으로 Blob을 비동기적으로 복사</span><span class="sxs-lookup"><span data-stu-id="87f36-117">Copies a blob asynchronously from one storage account to another</span></span> |

## <a name="next-steps"></a><span data-ttu-id="87f36-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="87f36-118">Next steps</span></span>

[<span data-ttu-id="87f36-119">VHD에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="87f36-119">Create a managed disk from a VHD</span></span>](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="87f36-120">관리 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="87f36-120">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="87f36-121">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="87f36-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="87f36-122">추가 가상 컴퓨터 및 관리 디스크 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87f36-122">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
