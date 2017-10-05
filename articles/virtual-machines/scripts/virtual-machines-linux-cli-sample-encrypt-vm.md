---
title: "Azure CLI 스크립트 샘플 - Linux VM 암호화 | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Linux VM 암호화"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 9388bce04e37d049301521f808cd8494c327e335
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="encrypt-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="ab8da-103">Azure에서 Linux 가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="ab8da-103">Encrypt a Linux virtual machine in Azure</span></span>

<span data-ttu-id="ab8da-104">이 스크립트는 보안 Azure Key Vault, 암호화 키, Azure Active Directory 서비스 주체 및 Linux VM(가상 컴퓨터)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Linux virtual machine (VM).</span></span> <span data-ttu-id="ab8da-105">그런 다음 Key Vault의 암호화 키 및 서비스 주체 자격 증명을 사용하여 VM을 암호화합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-105">The VM is then encrypted using the encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ab8da-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ab8da-106">Sample script</span></span>

<span data-ttu-id="ab8da-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "VM 디스크 암호화")]</span><span class="sxs-lookup"><span data-stu-id="ab8da-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_vm.sh "Encrypt VM disks")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="ab8da-108">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ab8da-108">Clean up deployment</span></span> 

<span data-ttu-id="ab8da-109">다음 명령을 실행하여 리소스 그룹, VM 및 모든 관련된 리소스를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ab8da-110">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ab8da-110">Script explanation</span></span>

<span data-ttu-id="ab8da-111">이 스크립트 다음 명령을 사용하여 리소스 그룹, Azure Key Vault, 서비스 주체, 가상 컴퓨터 및 모든 관련 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-111">This script uses the following commands to create a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="ab8da-112">테이블에 있는 각 명령은 명령에 해당하는 문서에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ab8da-113">명령</span><span class="sxs-lookup"><span data-stu-id="ab8da-113">Command</span></span> | <span data-ttu-id="ab8da-114">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ab8da-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ab8da-115">az group create</span><span class="sxs-lookup"><span data-stu-id="ab8da-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ab8da-116">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ab8da-117">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="ab8da-117">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="ab8da-118">암호화 키와 같은 보안 데이터를 저장하기 위한 Azure Key Vault를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-118">Creates an Azure Key Vault to store secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="ab8da-119">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="ab8da-119">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="ab8da-120">Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-120">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="ab8da-121">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="ab8da-121">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="ab8da-122">암호화 키를 안전하게 인증하고 암호화 키에 대한 액세스를 제어하기 위한 Azure Active Directory 서비스 주체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-122">Creates an Azure Active Directory service principal to securely authenticate and control access to encryption keys.</span></span> |
| [<span data-ttu-id="ab8da-123">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="ab8da-123">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="ab8da-124">서비스 주체에 암호화 키에 대한 액세스 권한을 부여하기 위해 Key Vault에 대한 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-124">Sets permissions on the Key Vault to grant the service principal access to encryption keys.</span></span> |
| [<span data-ttu-id="ab8da-125">az vm create</span><span class="sxs-lookup"><span data-stu-id="ab8da-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ab8da-126">가상 컴퓨터를 만들고 네트워크 카드, 가상 네트워크, 서브넷 및 NSG에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="ab8da-127">또한 이 명령은 사용할 가상 컴퓨터 이미지와 관리 자격 증명을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="ab8da-128">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="ab8da-128">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="ab8da-129">서비스 주체 자격 증명 및 암호화 키를 사용하여 VM에 대해 암호화를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-129">Enables encryption on a VM using the service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="ab8da-130">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="ab8da-130">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="ab8da-131">VM 암호화 프로세스의 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-131">Shows the status of the VM encryption process.</span></span> |
| [<span data-ttu-id="ab8da-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="ab8da-132">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ab8da-133">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-133">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ab8da-134">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ab8da-134">Next steps</span></span>

<span data-ttu-id="ab8da-135">Azure CLI에 대한 자세한 내용은 [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ab8da-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ab8da-136">추가 가상 컴퓨터 CLI 스크립트 샘플은 [Azure Linux VM 설명서](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ab8da-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
