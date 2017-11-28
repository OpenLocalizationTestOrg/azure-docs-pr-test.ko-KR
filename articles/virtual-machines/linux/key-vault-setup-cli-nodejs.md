---
title: "Azure CLI 1.0을 사용하여 Linux VM에 대한 Key Vault 설정 | Microsoft Docs"
description: "Azure CLI 1.0을 사용하여 Azure Resource Manager에서 사용할 Key Vault를 설정하는 방법"
services: virtual-machines-linux
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: bccdd5ab-5ccf-4760-9039-92c6eafb15bd
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/24/2017
ms.author: singhkay
ms.openlocfilehash: fed612a354d45f34619f2a66bd40d78740c43ac7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-the-azure-cli-10"></a><span data-ttu-id="c446a-103">Azure CLI 1.0을 사용하여 Azure Resource Manager에서 가상 컴퓨터에 대한 Key Vault 설정</span><span class="sxs-lookup"><span data-stu-id="c446a-103">Set up Key Vault for virtual machines in Azure Resource Manager with the Azure CLI 1.0</span></span>
<span data-ttu-id="c446a-104">Azure Resource Manager 스택에서 암호/인증서는 Key Vault의 리소스 공급자가 제공하는 리소스로 모델링됩니다.</span><span class="sxs-lookup"><span data-stu-id="c446a-104">In the Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by the resource provider of Key Vault.</span></span> <span data-ttu-id="c446a-105">Azure 주요 자격 증명 모음에 대한 자세한 내용을 보려면 [Azure 주요 자격 증명 모음이란?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c446a-105">To learn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="c446a-106">주요 자격 증명 모음을 Azure Resource Manager 가상 컴퓨터에서 사용하려면 주요 자격 증명에 대한 *EnabledForDeployment* 속성을 true로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c446a-106">In order for Key Vault to be used with Azure Resource Manager virtual machines, the *EnabledForDeployment* property on Key Vault must be set to true.</span></span> <span data-ttu-id="c446a-107">다양한 클라이언트에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c446a-107">You can do this in various clients.</span></span> <span data-ttu-id="c446a-108">이 문서에서는 Azure Virtual Machines에서 사용할 Key Vault를 설정하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c446a-108">This article shows you how to set up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="c446a-109">태스크를 완료하기 위한 CLI 버전</span><span class="sxs-lookup"><span data-stu-id="c446a-109">CLI versions to complete the task</span></span>
<span data-ttu-id="c446a-110">다음 CLI 버전 중 하나를 사용하여 태스크를 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c446a-110">You can complete the task using one of the following CLI versions</span></span>

- <span data-ttu-id="c446a-111">[Azure CLI 1.0](#quick-commands) - 클래식 및 리소스 관리 배포 모델용 CLI(이 문서)</span><span class="sxs-lookup"><span data-stu-id="c446a-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c446a-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - 리소스 관리 배포 모델용 차세대 CLI</span><span class="sxs-lookup"><span data-stu-id="c446a-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>

## <a name="use-cli-10-to-set-up-key-vault"></a><span data-ttu-id="c446a-113">CLI 1.0을 사용하여 Key Vault 설정</span><span class="sxs-lookup"><span data-stu-id="c446a-113">Use CLI 1.0 to set up Key Vault</span></span>
<span data-ttu-id="c446a-114">CLI(명령줄 인터페이스)를 사용하여 주요 자격 증명 모음을 만들려면 [CLI를 사용하여 주요 자격 증명 모음 관리](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c446a-114">To create a key vault by using the command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="c446a-115">CLI 1.0의 경우 먼저 Key Vault를 만든 다음 배포 정책을 할당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c446a-115">For CLI 1.0, you have to create the key vault before you assign the deployment policy.</span></span> <span data-ttu-id="c446a-116">다음 명령을 사용하여 정책을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c446a-116">You can then assign the policy by using the following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-to-set-up-key-vault"></a><span data-ttu-id="c446a-117">템플릿을 사용하여 주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="c446a-117">Use templates to set up Key Vault</span></span>
<span data-ttu-id="c446a-118">템플릿을 사용하는 경우 `enabledForDeployment` 속성을 주요 자격 증명 모음 리소스에 대한 `true`로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c446a-118">When you use a template, you need to set the `enabledForDeployment` property to `true` for the Key Vault resource.</span></span>

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

<span data-ttu-id="c446a-119">템플릿을 사용하여 주요 자격 증명 모음을 만들 때 구성할 수 있는 다른 옵션에 대해서는 [주요 자격 증명 모음 만들기](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c446a-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
