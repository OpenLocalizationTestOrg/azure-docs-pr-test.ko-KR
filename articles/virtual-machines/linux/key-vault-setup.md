---
title: "Linux Vm에 대 한 Azure 키 자격 증명 모음을 aaaSet | Microsoft Docs"
description: "어떻게 키 자격 증명 모음을 사용 하는 Azure 리소스 관리자 가상 컴퓨터와 함께 사용할 tooset hello CLI 2.0."
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
ms.openlocfilehash: a5dc1fbe59a71b4456ba5b9bbacdb90440064757
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-key-vault-for-virtual-machines-with-hello-azure-cli-20"></a><span data-ttu-id="30700-103">키 자격 증명 모음을 사용 하 여 가상 컴퓨터 tooset Azure CLI 2.0 hello 하는 방법</span><span class="sxs-lookup"><span data-stu-id="30700-103">How tooset up Key Vault for virtual machines with hello Azure CLI 2.0</span></span>

<span data-ttu-id="30700-104">Hello Azure 리소스 관리자 스택의 비밀/인증서는 키 자격 증명 모음에서 제공 되는 리소스 그룹으로 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="30700-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by Key Vault.</span></span> <span data-ttu-id="30700-105">Azure 키 자격 증명 모음에 대 한 자세한 toolearn 참조 [Azure 키 자격 증명 모음 이란?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="30700-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="30700-106">주요 자격 증명 모음 toobe vm이 Azure 리소스 관리자 사용에 대 한 순서로 hello *EnabledForDeployment* tootrue 속성 주요 자격 증명 모음을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30700-106">In order for Key Vault toobe used with Azure Resource Manager VMs, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="30700-107">이 문서에서는 키 자격 증명 모음을 사용 하 여 Azure 가상 컴퓨터 (Vm)를 사용 하기 위해 tooset Azure CLI 2.0 hello 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="30700-107">This article shows you how tooset up Key Vault for use with Azure virtual machines (VMs) using hello Azure CLI 2.0.</span></span> <span data-ttu-id="30700-108">Hello로 다음이 단계를 수행할 수도 있습니다 [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="30700-108">You can also perform these steps with hello [Azure CLI 1.0](key-vault-setup-cli-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="30700-109">이 단계는 tooperform, 필요한 hello 최신 [Azure CLI 2.0](/cli/azure/install-az-cli2) 설치 하 고 tooan Azure 계정을 사용 하 여 로그인 [az 로그인](/cli/azure/#login)합니다.</span><span class="sxs-lookup"><span data-stu-id="30700-109">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="30700-110">주요 자격 증명 모음 만들기</span><span class="sxs-lookup"><span data-stu-id="30700-110">Create a Key Vault</span></span>
<span data-ttu-id="30700-111">키 자격 증명 모음 만들기 및 할당 된 hello 배포 정책을 [az keyvault 만들](/cli/azure/keyvault#create)합니다.</span><span class="sxs-lookup"><span data-stu-id="30700-111">Create a key vault and assign hello deployment policy with [az keyvault create](/cli/azure/keyvault#create).</span></span> <span data-ttu-id="30700-112">hello 다음 예제에서는 키 자격 증명 모음 이름이 `myKeyVault` hello에 `myResourceGroup` 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="30700-112">hello following example creates a key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault create -l westus -n myKeyVault -g myResourceGroup --enabled-for-deployment true
```

## <a name="update-a-key-vault-for-use-with-vms"></a><span data-ttu-id="30700-113">VM과 함께 사용할 Key Vault를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="30700-113">Update a Key Vault for use with VMs</span></span>
<span data-ttu-id="30700-114">기존 키 자격 증명 모음에 hello 배포 정책 설정 [az keyvault 업데이트](/cli/azure/keyvault#update)합니다.</span><span class="sxs-lookup"><span data-stu-id="30700-114">Set hello deployment policy on an existing key vault with [az keyvault update](/cli/azure/keyvault#update).</span></span> <span data-ttu-id="30700-115">hello 다음 업데이트 hello 라는 주요 자격 증명 모음 `myKeyVault` hello에 `myResourceGroup` 리소스 그룹:</span><span class="sxs-lookup"><span data-stu-id="30700-115">hello following updates hello key vault named `myKeyVault` in hello `myResourceGroup` resource group:</span></span>

```azurecli
az keyvault update -n myKeyVault -g myResourceGroup --set properties.enabledForDeployment=true
```

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="30700-116">키 자격 증명 모음을 사용 하 여 템플릿 tooset</span><span class="sxs-lookup"><span data-stu-id="30700-116">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="30700-117">Tooset hello 템플릿을 사용 하는 경우 해야 `enabledForDeployment` 속성 너무`true` 다음과 같이 hello 키 자격 증명 모음 리소스에 대 한:</span><span class="sxs-lookup"><span data-stu-id="30700-117">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource as follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="30700-118">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30700-118">Next steps</span></span>
<span data-ttu-id="30700-119">템플릿을 사용하여 Key Vault을 만들 때 구성할 수 있는 다른 옵션에 대해서는 [주요 자격 증명 모음 만들기](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30700-119">For other options that you can configure when you create a Key Vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
