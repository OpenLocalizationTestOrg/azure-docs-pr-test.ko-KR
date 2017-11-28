---
title: "CLI 스크립트 샘플-aaaAzure hello의 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만드는 구독과 동일한 구독 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플-hello의 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만들려면 동일한 구독"
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
ms.openlocfilehash: 1e792fdbb7daea92bf6a6589a5d8aab5b9b5a670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-hello-same-subscription-with-cli"></a><span data-ttu-id="c2b5e-103">Hello의 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만들 CLI와 동일한 구독</span><span class="sxs-lookup"><span data-stu-id="c2b5e-103">Create a managed disk from a VHD file in a storage account in hello same subscription with CLI</span></span>

<span data-ttu-id="c2b5e-104">이 스크립트는 hello의 저장소 계정에 VHD 파일에서 관리 되는 디스크를 만듭니다 동일한 구독 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b5e-104">This script creates a managed disk from a VHD file in a storage account in hello same subscription.</span></span> <span data-ttu-id="c2b5e-105">이 스크립트 tooimport는 특수화 된 (하지 일반화/sysprepped) VHD toomanaged OS 디스크 toocreate 가상 컴퓨터를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b5e-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="c2b5e-106">또는 tooimport 데이터 VHD toomanaged 데이터 디스크를 사용 하세요.</span><span class="sxs-lookup"><span data-stu-id="c2b5e-106">Or, use it tooimport a data VHD toomanaged data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c2b5e-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="c2b5e-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="c2b5e-108">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="c2b5e-108">Script explanation</span></span>

<span data-ttu-id="c2b5e-109">이 스크립트 명령 toocreate 다음 VHD에서 관리 되는 디스크를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b5e-109">This script uses following commands toocreate a managed disk from a VHD.</span></span> <span data-ttu-id="c2b5e-110">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b5e-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c2b5e-111">명령</span><span class="sxs-lookup"><span data-stu-id="c2b5e-111">Command</span></span> | <span data-ttu-id="c2b5e-112">참고 사항</span><span class="sxs-lookup"><span data-stu-id="c2b5e-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c2b5e-113">az disk create</span><span class="sxs-lookup"><span data-stu-id="c2b5e-113">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="c2b5e-114">VHD의 URI를 사용 하 여 hello의 저장소 계정에 관리 되는 디스크를 만듭니다 동일한 구독</span><span class="sxs-lookup"><span data-stu-id="c2b5e-114">Creates a managed disk using URI of a VHD in a storage account in hello same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c2b5e-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c2b5e-115">Next steps</span></span>

[<span data-ttu-id="c2b5e-116">관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="c2b5e-116">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="c2b5e-117">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b5e-117">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c2b5e-118">추가 가상 컴퓨터와 관리 되는 디스크 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Linux VM 설명서](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="c2b5e-118">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
