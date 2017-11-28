---
title: "Azure Resource Manager에서 Windows VM에 대한 Key Vault 설정 | Microsoft Docs"
description: "Azure Resource Manager에서 사용할 주요 자격 증명 모음을 설정하는 방법"
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33a483e2-cfbc-4c62-a588-5d9fd52491e2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/24/2017
ms.author: kasing
ms.openlocfilehash: a5083a5216efbfd76fd912ec48c2f0ec3b30c4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="26308-103">Azure Resource Manager에서 가상 컴퓨터에 대한 주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="26308-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="26308-104">Azure Resource Manager 스택에서 비밀/인증서는 주요 자격 증명 모음 리소스 공급자가 제공하는 리소스로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="26308-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="26308-105">주요 자격 증명 모음에 대한 자세한 내용을 보려면 [Azure 주요 자격 증명 모음이란?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="26308-105">To learn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="26308-106">주요 자격 증명 모음을 Azure Resource Manager 가상 컴퓨터에서 사용하려면 주요 자격 증명에 대한 **EnabledForDeployment** 속성을 true로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26308-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the **EnabledForDeployment** property on Key Vault must be set to true.</span></span> <span data-ttu-id="26308-107">다양한 클라이언트에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26308-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="26308-108">주요 자격 증명 모음은 가상 컴퓨터와 동일한 구독 및 위치에 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26308-108">The Key Vault needs to be created in the same subscription and location as the Virtual Machine.</span></span>
>
>

## <a name="use-powershell-to-set-up-key-vault"></a><span data-ttu-id="26308-109">PowerShell을 사용하여 주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="26308-109">Use PowerShell to set up Key Vault</span></span>
<span data-ttu-id="26308-110">PowerShell을 사용하여 주요 자격 증명 모음을 만들려면 [Azure 주요 자격 증명 모음 시작](../../key-vault/key-vault-get-started.md#vault)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26308-110">To create a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="26308-111">새 주요 자격 증명의 경우 다음 PowerShell cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26308-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="26308-112">기존 주요 자격 증명의 경우 다음 PowerShell cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26308-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-to-set-up-key-vault"></a><span data-ttu-id="26308-113">CLI를 사용하여 주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="26308-113">Us CLI to set up Key Vault</span></span>
<span data-ttu-id="26308-114">CLI(명령줄 인터페이스)를 사용하여 주요 자격 증명 모음을 만들려면 [CLI를 사용하여 주요 자격 증명 모음 관리](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26308-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="26308-115">CLI의 경우 먼저 주요 자격 증명 모음을 만든 다음 배포 정책을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26308-115">For CLI, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="26308-116">다음 명령을 사용하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26308-116">You can do this by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="26308-117">템플릿을 사용하여 주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="26308-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="26308-118">템플릿을 사용하는 경우 `enabledForDeployment` 속성을 주요 자격 증명 모음 리소스에 대한 `true`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="26308-118">While you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="26308-119">템플릿을 사용하여 주요 자격 증명 모음을 만들 때 구성할 수 있는 다른 옵션에 대해서는 [주요 자격 증명 모음 만들기](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="26308-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
