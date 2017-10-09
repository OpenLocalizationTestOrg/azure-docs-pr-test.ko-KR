---
title: "CLI 스크립트 샘플-다른 지역의 VHD tooa 저장소 계정으로 내보내기/복사 스냅숏 aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-동일 하거나 다른 구독에서 VHD tooa 저장소 계정으로 내보내기/복사 스냅숏"
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
ms.openlocfilehash: 945f83d2ed715642156ca7b252af08559c652b14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="e44a8-103">CLI 사용 하 여 다른 영역에서 VHD tooa 저장소 계정으로 관리 되는 스냅숏 내보내기/복사</span><span class="sxs-lookup"><span data-stu-id="e44a8-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="e44a8-104">이 스크립트는 관리 되는 스냅숏 tooa 저장소 계정을 다른 지역에 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e44a8-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="e44a8-105">먼저 hello hello 스냅숏의 SAS URI를 생성 하 고 다음 toocopy 사용 것 tooa 다른 지역의 저장소 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="e44a8-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="e44a8-106">재해 복구를 위해 다른 지역에이 스크립트 toomaintain 백업을 관리 되는 디스크를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44a8-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e44a8-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="e44a8-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="e44a8-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="e44a8-108">Script explanation</span></span>

<span data-ttu-id="e44a8-109">다음 명령을 toogenerate 사용 하 여 관리 되는 스냅숏 및 복사본이 hello에 대 한 SAS URI 스냅숏 tooa 저장소 계정의 SAS URI를 사용 하 여이 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="e44a8-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="e44a8-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="e44a8-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e44a8-111">명령</span><span class="sxs-lookup"><span data-stu-id="e44a8-111">Command</span></span> | <span data-ttu-id="e44a8-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="e44a8-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e44a8-113">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="e44a8-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="e44a8-114">Tooon 온-프레미스 기본 VHD 파일 tooa 저장소 계정을 사용 하는 toocopy 되거나 다운로드 되는 읽기 전용 SAS를 생성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e44a8-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="e44a8-115">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="e44a8-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="e44a8-116">저장소 계정 tooanother 하나에서 blob를 비동기적으로 복사</span><span class="sxs-lookup"><span data-stu-id="e44a8-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e44a8-117">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e44a8-117">Next steps</span></span>

[<span data-ttu-id="e44a8-118">VHD에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="e44a8-118">Create a managed disk from a VHD</span></span>](virtual-machines-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="e44a8-119">관리 디스크에서 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="e44a8-119">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="e44a8-120">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="e44a8-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e44a8-121">추가 가상 컴퓨터와 관리 되는 디스크 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="e44a8-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
