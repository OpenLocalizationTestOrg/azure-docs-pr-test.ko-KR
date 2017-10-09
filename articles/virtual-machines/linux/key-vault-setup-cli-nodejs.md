---
title: "Linux Vm에 대 한 자격 증명 모음 키를 Azure CLI 1.0 hello로 aaaSet | Microsoft Docs"
description: "어떻게 키 자격 증명 모음을 사용 하는 Azure 리소스 관리자 가상 컴퓨터와 함께 사용할 tooset hello Azure CLI 1.0입니다."
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
ms.openlocfilehash: 275022e4e7e26d7363784c289dd7512047c07bad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-key-vault-for-virtual-machines-in-azure-resource-manager-with-hello-azure-cli-10"></a><span data-ttu-id="16b2d-103">Azure CLI 1.0 hello로 Azure 리소스 관리자의 가상 컴퓨터에 대 한 키 자격 증명 모음 설정</span><span class="sxs-lookup"><span data-stu-id="16b2d-103">Set up Key Vault for virtual machines in Azure Resource Manager with hello Azure CLI 1.0</span></span>
<span data-ttu-id="16b2d-104">Hello Azure 리소스 관리자 스택의 비밀/인증서는 키 자격 증명 모음 hello 리소스 공급자가 제공 되는 리소스 그룹으로 모델링 됩니다.</span><span class="sxs-lookup"><span data-stu-id="16b2d-104">In hello Azure Resource Manager stack, secrets/certificates are modeled as resources that are provided by hello resource provider of Key Vault.</span></span> <span data-ttu-id="16b2d-105">Azure 키 자격 증명 모음에 대 한 자세한 toolearn 참조 [Azure 키 자격 증명 모음 이란?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="16b2d-105">toolearn more about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md)</span></span> <span data-ttu-id="16b2d-106">Azure 리소스 관리자 가상 컴퓨터와 함께 사용 되는 주요 자격 증명 모음 toobe에 대 한 순서로 hello *EnabledForDeployment* tootrue 속성 주요 자격 증명 모음을 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b2d-106">In order for Key Vault toobe used with Azure Resource Manager virtual machines, hello *EnabledForDeployment* property on Key Vault must be set tootrue.</span></span> <span data-ttu-id="16b2d-107">다양한 클라이언트에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b2d-107">You can do this in various clients.</span></span> <span data-ttu-id="16b2d-108">이 문서에서는 Azure 가상 컴퓨터와 함께 사용 하기 위해 키 자격 증명 모음을 tooset 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b2d-108">This article shows you how tooset up Key Vault for use with Azure Virtual Machines.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="16b2d-109">CLI 버전 toocomplete hello 작업</span><span class="sxs-lookup"><span data-stu-id="16b2d-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="16b2d-110">Hello CLI 버전을 다음 중 하나를 사용 하 여 hello 작업을 완료할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b2d-110">You can complete hello task using one of hello following CLI versions</span></span>

- <span data-ttu-id="16b2d-111">[Azure CLI 1.0](#quick-commands) – 우리의 CLI 모델에 대 한 hello 클래식 및 리소스 관리 배포 (이 문서)</span><span class="sxs-lookup"><span data-stu-id="16b2d-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="16b2d-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -우리의 차세대 CLI hello 리소스 관리 배포 모델에 대 한</span><span class="sxs-lookup"><span data-stu-id="16b2d-112">[Azure CLI 2.0](../windows/key-vault-setup.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="use-cli-10-tooset-up-key-vault"></a><span data-ttu-id="16b2d-113">CLI 1.0 tooset 키 자격 증명 모음을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="16b2d-113">Use CLI 1.0 tooset up Key Vault</span></span>
<span data-ttu-id="16b2d-114">hello CLI (명령줄 인터페이스)를 사용 하 여 주요 자격 증명 모음 toocreate 참조 [관리 키 자격 증명 모음 CLI를 사용 하 여](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault)합니다.</span><span class="sxs-lookup"><span data-stu-id="16b2d-114">toocreate a key vault by using hello command-line interface (CLI), see [Manage Key Vault using CLI](../../key-vault/key-vault-manage-with-cli2.md#create-a-key-vault).</span></span>

<span data-ttu-id="16b2d-115">CLI 1.0에 대 한 hello 배포 정책을 지정 하기 전에 toocreate hello 키 자격 증명 모음이 있는지 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b2d-115">For CLI 1.0, you have toocreate hello key vault before you assign hello deployment policy.</span></span> <span data-ttu-id="16b2d-116">다음 명령을 hello를 사용 하 여 hello 정책 그런 다음 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="16b2d-116">You can then assign hello policy by using hello following command:</span></span>

    azure keyvault set-policy ContosoKeyVault –enabled-for-deployment true

## <a name="use-templates-tooset-up-key-vault"></a><span data-ttu-id="16b2d-117">키 자격 증명 모음을 사용 하 여 템플릿 tooset</span><span class="sxs-lookup"><span data-stu-id="16b2d-117">Use templates tooset up Key Vault</span></span>
<span data-ttu-id="16b2d-118">Tooset hello 템플릿을 사용 하는 경우 해야 `enabledForDeployment` 속성 너무`true` hello 키 자격 증명 모음 리소스에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="16b2d-118">When you use a template, you need tooset hello `enabledForDeployment` property too`true` for hello Key Vault resource.</span></span>

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

<span data-ttu-id="16b2d-119">템플릿을 사용하여 주요 자격 증명 모음을 만들 때 구성할 수 있는 다른 옵션에 대해서는 [주요 자격 증명 모음 만들기](https://azure.microsoft.com/documentation/templates/101-key-vault-create/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="16b2d-119">For other options that you can configure when you create a key vault by using templates, see [Create a key vault](https://azure.microsoft.com/documentation/templates/101-key-vault-create/).</span></span>
