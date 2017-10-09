---
title: "키 자격 증명 모음에 대 한 Windows Vm이 Azure 리소스 관리자를 aaaSet | Microsoft Docs"
description: "어떻게 Azure 리소스 관리자 가상 컴퓨터와 함께 사용 하기 위해 키 자격 증명 모음을 tooset 합니다."
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
ms.openlocfilehash: 53bbe90708202ecfdcf754822d04bf2469631f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager"></a><span data-ttu-id="c883b-103">Azure Resource Manager에서 가상 컴퓨터에 대한 주요 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="c883b-103">Set up Key Vault for virtual machines in Azure Resource Manager</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-rm-include.md)]

<span data-ttu-id="c883b-104">Azure 리소스 관리자 스택의 비밀/인증서는 키 자격 증명 모음 hello 리소스 공급자가 제공 되는 리소스 그룹으로 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-104">In Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="c883b-105">주요 자격 증명에 대 한 자세한 toolearn 참조 [Azure 키 자격 증명 모음 이란?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c883b-105">toolearn more about Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span>

> [!NOTE]
> 1. <span data-ttu-id="c883b-106">Azure 리소스 관리자 가상 컴퓨터와 함께 사용 되는 주요 자격 증명 모음 toobe에 대 한 순서로 hello **EnabledForDeployment** tootrue 속성 주요 자격 증명 모음을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello **EnabledForDeployment** property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="c883b-107">다양한 클라이언트에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-107">You can do this in various clients.</span></span>
> 2. <span data-ttu-id="c883b-108">가상 컴퓨터를 hello 대로 toobe에서 만든 hello 주요 자격 증명 모음 요구 hello 동일한 구독 및 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-108">hello Key Vault needs toobe created in hello same subscription and location as hello Virtual Machine.</span></span>
>
>

## <a name="use-powershell-tooset-up-key-vault"></a><span data-ttu-id="c883b-109">키 자격 증명 모음을 사용 하 여 PowerShell tooset</span><span class="sxs-lookup"><span data-stu-id="c883b-109">Use PowerShell tooset up Key Vault</span></span>
<span data-ttu-id="c883b-110">PowerShell을 사용 하 여 주요 자격 증명 모음 toocreate 참조 [Azure 키 자격 증명 모음 시작](../../key-vault/key-vault-get-started.md#vault)합니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-110">toocreate a key vault by using PowerShell, see [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md#vault).</span></span>

<span data-ttu-id="c883b-111">새 주요 자격 증명의 경우 다음 PowerShell cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-111">For new key vaults, you can use this PowerShell cmdlet:</span></span>

    New-AzureRmKeyVault -VaultName 'ContosoKeyVault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East Asia' -EnabledForDeployment

<span data-ttu-id="c883b-112">기존 주요 자격 증명의 경우 다음 PowerShell cmdlet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-112">For existing key vaults, you can use this PowerShell cmdlet:</span></span>

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'ContosoKeyVault' -EnabledForDeployment

## <a name="us-cli-tooset-up-key-vault"></a><span data-ttu-id="c883b-113">Us CLI tooset 키 자격 증명 모음을</span><span class="sxs-lookup"><span data-stu-id="c883b-113">Us CLI tooset up Key Vault</span></span>
<span data-ttu-id="c883b-114">hello CLI (명령줄 인터페이스)를 사용 하 여 주요 자격 증명 모음 toocreate 참조 [관리 키 자격 증명 모음 CLI를 사용 하 여](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)합니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="c883b-115">CLI에 대 한 hello 배포 정책을 지정 하기 전에 toocreate hello 키 자격 증명 모음이 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-115">For CLI, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="c883b-116">다음 명령을 hello를 사용 하 여이 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-116">You can do this by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="c883b-117">키 자격 증명 모음을 사용 하 여 템플릿 tooset</span><span class="sxs-lookup"><span data-stu-id="c883b-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="c883b-118">Tooset hello 서식 파일을 사용 하는 동안 필요한 `enabledForDeployment` 속성 너무`true` hello 키 자격 증명 모음 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="c883b-118">While you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="c883b-119">템플릿을 사용하여 주요 자격 증명 모음을 만들 때 구성할 수 있는 다른 옵션에 대해서는 [주요 자격 증명 모음 만들기](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c883b-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
