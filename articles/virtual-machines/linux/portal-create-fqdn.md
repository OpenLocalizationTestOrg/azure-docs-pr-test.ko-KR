---
title: "Azure Portal에서 Linux VM에 대한 FQDN 만들기 | Microsoft Docs"
description: "Azure Portal에서 가상 컴퓨터를 기반으로 한 Resource Manager에 대한 정규화된 도메인 이름 또는 FQDN을 만드는 방법에 대해 알아봅니다."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 2cd6c249-a737-4a0a-b5ba-e1c09e551b30
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 49bfec791fcca3feabc4eb280cefd7faada0ea31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-linux-vm"></a><span data-ttu-id="60906-103">Linux VM용 Azure Portal에서 정규화된 도메인 이름 만들기</span><span class="sxs-lookup"><span data-stu-id="60906-103">Create a fully qualified domain name in the Azure portal for a Linux VM</span></span>

<span data-ttu-id="60906-104">[Azure Portal](https://portal.azure.com)에서 VM(가상 컴퓨터)을 만들 때, 가상 컴퓨터의 공용 IP 리소스가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="60906-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="60906-105">이 IP 주소를 사용하여 VM에 원격으로 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="60906-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="60906-106">포털에서 [정규화된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) 또는 FQDN을 만들지는 않지만 VM을 만들면 이름을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60906-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once the VM is created.</span></span> <span data-ttu-id="60906-107">이 문서에서는 DNS 이름 또는 FQDN을 만드는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="60906-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="60906-108">FQDN 만들기</span><span class="sxs-lookup"><span data-stu-id="60906-108">Create a FQDN</span></span>
<span data-ttu-id="60906-109">이 문서에서는 사용자가 VM을 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="60906-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="60906-110">필요한 경우 [포털에서](quick-create-portal.md) 또는 [Azure CLI를 사용하여](quick-create-cli.md) VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60906-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with the Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="60906-111">VM이 실행되면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="60906-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="60906-112">이제 `ssh azureuser@mydns.westus.cloudapp.azure.com`을 사용하는 경우처럼 이 DNS 이름을 사용하여 원격으로 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60906-112">You can now connect remotely to the VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60906-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="60906-113">Next steps</span></span>
<span data-ttu-id="60906-114">VM에는 공용 IP 및 DNS 이름이 있으므로 nginx, MongoDB, Docker와 같은 일반적인 응용 프로그램 프레임워크 또는 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60906-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="60906-115">또한 Azure 배포 구축에 대한 팁은 [Resource Manager 사용](../../azure-resource-manager/resource-group-overview.md)에서 자세히 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="60906-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

