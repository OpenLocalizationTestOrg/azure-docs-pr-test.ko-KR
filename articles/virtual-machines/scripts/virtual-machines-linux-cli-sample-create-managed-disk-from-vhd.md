---
title: "Azure CLI 스크립트 샘플 - 동일한 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - 동일한 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기"
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
ms.openlocfilehash: 448636e87db126defc804a613bb61ff19a086ad9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-the-same-subscription-with-cli"></a><span data-ttu-id="2b7b1-103">CLI를 사용하여 동일한 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="2b7b1-103">Create a managed disk from a VHD file in a storage account in the same subscription with CLI</span></span>

<span data-ttu-id="2b7b1-104">이 스크립트는 동일한 구독에 있는 저장소 계정의 VHD 파일에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b7b1-104">This script creates a managed disk from a VHD file in a storage account in the same subscription.</span></span> <span data-ttu-id="2b7b1-105">이 스크립트를 사용하여 관리 OS 디스크에 특수화된(일반화/sysprep되지 않음) VHD를 가져와 가상 컴퓨터를 만듭니다</span><span class="sxs-lookup"><span data-stu-id="2b7b1-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="2b7b1-106">또는 데이터 VHD를 관리되는 데이터 디스크로 가져오는 데 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2b7b1-106">Or, use it to import a data VHD to managed data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2b7b1-107">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="2b7b1-107">Sample script</span></span>

<span data-ttu-id="2b7b1-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "VHD에서 관리 디스크 만들기")]</span><span class="sxs-lookup"><span data-stu-id="2b7b1-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="2b7b1-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="2b7b1-109">Script explanation</span></span>

<span data-ttu-id="2b7b1-110">이 스크립트에서는 다음 명령을 사용하여 VHD에서 관리 디스크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b7b1-110">This script uses following commands to create a managed disk from a VHD.</span></span> <span data-ttu-id="2b7b1-111">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b7b1-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2b7b1-112">명령</span><span class="sxs-lookup"><span data-stu-id="2b7b1-112">Command</span></span> | <span data-ttu-id="2b7b1-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="2b7b1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2b7b1-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="2b7b1-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="2b7b1-115">동일한 구독에 있는 저장소 계정의 VHD URI를 사용하여 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="2b7b1-115">Creates a managed disk using URI of a VHD in a storage account in the same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b7b1-116">다음 단계</span><span class="sxs-lookup"><span data-stu-id="2b7b1-116">Next steps</span></span>

[<span data-ttu-id="2b7b1-117">관리 디스크를 OS 디스크로 연결하여 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="2b7b1-117">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="2b7b1-118">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2b7b1-118">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2b7b1-119">추가 가상 컴퓨터 및 관리 디스크 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b7b1-119">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
