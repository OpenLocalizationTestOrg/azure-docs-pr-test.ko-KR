---
title: "Windows VM을 암호화 하는 CLI 스크립트 샘플-aaaAzure | Microsoft Docs"
description: "Azure CLI 스크립트 샘플 - Windows VM 암호화"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/02/2017
ms.author: iainfou
ms.openlocfilehash: 7a9928467f818cd5358d3d19bff5129d8fa21313
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="encrypt-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="ffbb7-103">Azure에서 Windows 가상 컴퓨터 암호화</span><span class="sxs-lookup"><span data-stu-id="ffbb7-103">Encrypt a Windows virtual machine in Azure</span></span>

<span data-ttu-id="ffbb7-104">이 스크립트는 보안 Azure Key Vault, 암호화 키, Azure Active Directory 서비스 주체 및 Windows VM(가상 컴퓨터)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-104">This script creates a secure Azure Key Vault, encryption keys, Azure Active Directory service principal, and a Windows virtual machine (VM).</span></span> <span data-ttu-id="ffbb7-105">그런 다음 VM hello 암호화 키를 키 자격 증명 모음 및 서비스 사용자 자격 증명 제공 hello를 사용 하 여 암호화 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-105">hello VM is then encrypted using hello encryption key from Key Vault and service principal credentials.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ffbb7-106">샘플 스크립트</span><span class="sxs-lookup"><span data-stu-id="ffbb7-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/encrypt-disks/encrypt_windows_vm.sh "Encrypt VM disks")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ffbb7-107">배포 정리</span><span class="sxs-lookup"><span data-stu-id="ffbb7-107">Clean up deployment</span></span> 

<span data-ttu-id="ffbb7-108">Hello 명령 tooremove hello 리소스 그룹, VM 및 관련 된 모든 리소스를 다음을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ffbb7-109">스크립트 설명</span><span class="sxs-lookup"><span data-stu-id="ffbb7-109">Script explanation</span></span>

<span data-ttu-id="ffbb7-110">이 스크립트는 다음 명령을 toocreate hello 리소스 그룹에서 Azure 키 자격 증명 모음 서비스 보안 주체를 가상 컴퓨터를 사용 하 고 모든 관련 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-110">This script uses hello following commands toocreate a resource group, Azure Key Vault, service principal, virtual machine, and all related resources.</span></span> <span data-ttu-id="ffbb7-111">Hello 테이블의 각 명령이 toocommand 특정 문서를 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ffbb7-112">명령</span><span class="sxs-lookup"><span data-stu-id="ffbb7-112">Command</span></span> | <span data-ttu-id="ffbb7-113">참고 사항</span><span class="sxs-lookup"><span data-stu-id="ffbb7-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ffbb7-114">az group create</span><span class="sxs-lookup"><span data-stu-id="ffbb7-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="ffbb7-115">모든 리소스가 저장되는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="ffbb7-116">az keyvault create</span><span class="sxs-lookup"><span data-stu-id="ffbb7-116">az keyvault create</span></span>](https://docs.microsoft.com/cli/azure/keyvault#create) | <span data-ttu-id="ffbb7-117">암호화 키와 같은 Azure 키 자격 증명 모음 toostore 보안 데이터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-117">Creates an Azure Key Vault toostore secure data such as encryption keys.</span></span> |
| [<span data-ttu-id="ffbb7-118">az keyvault key create</span><span class="sxs-lookup"><span data-stu-id="ffbb7-118">az keyvault key create</span></span>](https://docs.microsoft.com/cli/azure/keyvault/key#create) | <span data-ttu-id="ffbb7-119">Key Vault에서 암호화 키를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-119">Creates an encryption key in Key Vault.</span></span> |
| [<span data-ttu-id="ffbb7-120">az ad sp create-for-rbac</span><span class="sxs-lookup"><span data-stu-id="ffbb7-120">az ad sp create-for-rbac</span></span>](https://docs.microsoft.com/cli/azure/ad/sp#create-for-rbac) | <span data-ttu-id="ffbb7-121">Azure Active Directory 서비스를 인증 하 고 tooencryption 키 액세스를 제어 하는 주 toosecurely 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-121">Creates an Azure Active Directory service principal toosecurely authenticate and control access tooencryption keys.</span></span> |
| [<span data-ttu-id="ffbb7-122">az keyvault set-policy</span><span class="sxs-lookup"><span data-stu-id="ffbb7-122">az keyvault set-policy</span></span>](https://docs.microsoft.com/cli/azure/keyvault#set-policy) | <span data-ttu-id="ffbb7-123">Hello 서비스 보안 주체 액세스 tooencryption 키 hello 키 자격 증명 모음 toogrant에 사용 권한을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-123">Sets permissions on hello Key Vault toogrant hello service principal access tooencryption keys.</span></span> |
| [<span data-ttu-id="ffbb7-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="ffbb7-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="ffbb7-125">Hello 가상 컴퓨터를 만들고 toohello 네트워크 카드, 가상 네트워크, 서브넷 및 NSG를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="ffbb7-126">이 명령은 hello 가상 컴퓨터 이미지 toobe 사용 및 관리 자격 증명에도 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="ffbb7-127">az vm encryption enable</span><span class="sxs-lookup"><span data-stu-id="ffbb7-127">az vm encryption enable</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#enable) | <span data-ttu-id="ffbb7-128">Hello 서비스 사용자 자격 증명 및 암호화 키를 사용 하는 VM에서 암호화를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-128">Enables encryption on a VM using hello service principal credentials and encryption key.</span></span> |
| [<span data-ttu-id="ffbb7-129">az vm encryption show</span><span class="sxs-lookup"><span data-stu-id="ffbb7-129">az vm encryption show</span></span>](https://docs.microsoft.com/cli/azure/vm/encryption#show) | <span data-ttu-id="ffbb7-130">Hello hello VM 암호화 프로세스 상태가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-130">Shows hello status of hello VM encryption process.</span></span> |
| [<span data-ttu-id="ffbb7-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="ffbb7-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="ffbb7-132">모든 중첩 리소스를 포함한 리소스 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ffbb7-133">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ffbb7-133">Next steps</span></span>

<span data-ttu-id="ffbb7-134">Azure CLI hello에 대 한 자세한 내용은 참조 하십시오. [Azure CLI 설명서](https://docs.microsoft.com/cli/azure/overview)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-134">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ffbb7-135">가상 컴퓨터가 추가 CLI 스크립트 예제는 hello에서 확인할 수 있습니다 [Azure Windows VM 설명서](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="ffbb7-135">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%windows%2ftoc.json).</span></span>
