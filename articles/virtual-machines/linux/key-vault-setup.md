---
title: "Linux VM의 Azure Key Vault 설정 | Microsoft Docs"
description: "CLI 2.0을 사용하여 Azure Resource Manager 가상 컴퓨터에서 사용할 Key Vault를 설정하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: 2cc9b4c978e9a4deb0c8443c4b0f9e301a7cf492
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-key-vault-for-virtual-machines-with-the-azure-cli-20"></a><span data-ttu-id="9bcf0-103">Azure CLI 2.0을 사용하여 가상 컴퓨터의 Key Vault를 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="9bcf0-103">How to set up Key Vault for virtual machines with the Azure CLI 2.0</span></span>

<span data-ttu-id="9bcf0-104">Azure Resource Manager 스택에서 암호/인증서는 Key Vault에서 제공하는 리소스로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="9bcf0-105">Azure 주요 자격 증명 모음에 대한 자세한 내용을 보려면 [Azure 주요 자격 증명 모음이란?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="9bcf0-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="9bcf0-106">Key Vault을 Azure Resource Manager VM에서 사용하려면 Key Vault에 대한 *EnabledForDeployment* 속성을 true로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-106">In order for Key Vault to be used with Azure Resource Manager VMs, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="9bcf0-107">이 문서에서는 Azure CLI 2.0을 사용하여 Azure VM(가상 컴퓨터)에서 사용할 Key Vault를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-107">This article shows you how to set up Key Vault for use with Azure virtual machines (VMs) using the Azure CLI 2.0.</span></span> <span data-ttu-id="9bcf0-108">[Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)에서 이러한 단계를 수행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-108">You can also perform these steps with the [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="9bcf0-109">이러한 단계를 수행하려면 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2)을 설치하고 [az login](/cli/azure/#login)을 사용하여 Azure 계정에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-109">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="9bcf0-110">주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="9bcf0-110">Create a Key Vault</span></span>
<span data-ttu-id="9bcf0-111">[az keyvault create](/cli/azure/keyvault#create)를 사용하여 주요 자격 증명 모음을 만들고 배포 정책을 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-111">Create a key vault and assign the deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="9bcf0-112">다음 예제에서는 `myResourceGroup` 리소스 그룹에 `myKeyVault`이라는 주요 자격 증명 모음을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-112">The following example creates a key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="9bcf0-113">VM과 함께 사용할 Key Vault를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="9bcf0-114">[az keyvault update](/cli/azure/keyvault#update)를 사용하여 기존 주요 자격 증명 모음에 대한 배포 정책을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-114">Set the deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="9bcf0-115">다음에서는 `myResourceGroup` 리소스 그룹에 `myKeyVault`이라는 주요 자격 증명 모음을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-115">The following updates the key vault named `myKeyVault` in the `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="9bcf0-116">템플릿을 사용하여 주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="9bcf0-116">Use templates to set up Key Vault</span></span>
<span data-ttu-id="9bcf0-117">템플릿을 사용하는 경우 다음과 같이 `enabledForDeployment` 속성을 Key Vault 리소스의 `true`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-117">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource as follows:</span></span>

```json
{
    "type": "Microsoft.KeyVault/vaults",
    "name": "ContosoKeyVault",
    "apiVersion": "2015-06-01",
    "location": "<location-of-key-vault>",
    "properties": {
    "enabledForDeployment": "true",
    ....
    ....
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="9bcf0-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="9bcf0-118">Next steps</span></span>
<span data-ttu-id="9bcf0-119">템플릿을 사용하여 Key Vault을 만들 때 구성할 수 있는 다른 옵션에 대해서는 [주요 자격 증명 모음 만들기](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9bcf0-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
