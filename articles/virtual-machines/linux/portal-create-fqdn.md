---
title: "hello Azure 포털에서에서 Linux VM에 대 한 FQDN aaaCreate | Microsoft Docs"
description: "정규화 된 도메인 이름, 또는 리소스 관리자에 대 한 FQDN toocreate hello Azure 포털에서에서 가상 컴퓨터를 기반 하는 방법을 알아봅니다."
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
ms.openlocfilehash: 1494a0cb1caa62069c72096a739aee111ac8b383
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-qualified-domain-name-in-hello-azure-portal-for-a-linux-vm"></a><span data-ttu-id="e6ba6-103">Linux VM에 대 한 hello Azure 포털에서에서 정규화 된 도메인 이름 만들기</span><span class="sxs-lookup"><span data-stu-id="e6ba6-103">Create a fully qualified domain name in hello Azure portal for a Linux VM</span></span>

<span data-ttu-id="e6ba6-104">Hello에 가상 컴퓨터 (VM)를 만들 때 [Azure 포털](https://portal.azure.com), hello 가상 컴퓨터에 대 한 공용 IP 리소스를 자동으로 생성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-104">When you create a virtual machine (VM) in hello [Azure portal](https://portal.azure.com), a public IP resource for hello virtual machine is automatically created.</span></span> <span data-ttu-id="e6ba6-105">VM이 IP 주소 tooremotely 액세스 hello를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-105">You use this IP address tooremotely access hello VM.</span></span> <span data-ttu-id="e6ba6-106">Hello 포털을 만들지 않고 있지만 [정규화 된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), 또는 FQDN으로 추가할 수 있습니다 하나 만들어지면 hello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-106">Although hello portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can add one once hello VM is created.</span></span> <span data-ttu-id="e6ba6-107">이 문서에서는 hello 단계 toocreate DNS 이름 또는 FQDN을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-107">This article demonstrates hello steps toocreate a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="e6ba6-108">FQDN 만들기</span><span class="sxs-lookup"><span data-stu-id="e6ba6-108">Create a FQDN</span></span>
<span data-ttu-id="e6ba6-109">이 문서에서는 사용자가 VM을 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="e6ba6-110">필요한 경우 다음을 할 수 있습니다 [hello 포털에서 VM을 만듭니다](quick-create-portal.md) 또는 [hello Azure CLI로](quick-create-cli.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-110">If needed, you can [create a VM in hello portal](quick-create-portal.md) or [with hello Azure CLI](quick-create-cli.md).</span></span> <span data-ttu-id="e6ba6-111">VM이 실행되면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="e6ba6-112">연결할 수 있습니다. 원격으로 VM이이 DNS를 사용 하 여와 같은 이름을 toohello `ssh azureuser@mydns.westus.cloudapp.azure.com`합니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-112">You can now connect remotely toohello VM using this DNS name such as with `ssh azureuser@mydns.westus.cloudapp.azure.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6ba6-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e6ba6-113">Next steps</span></span>
<span data-ttu-id="e6ba6-114">VM에는 공용 IP 및 DNS 이름이 있으므로 nginx, MongoDB, Docker와 같은 일반적인 응용 프로그램 프레임워크 또는 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as nginx, MongoDB, Docker, etc.</span></span>

<span data-ttu-id="e6ba6-115">또한 Azure 배포 구축에 대한 팁은 [Resource Manager 사용](../../azure-resource-manager/resource-group-overview.md)에서 자세히 읽어볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6ba6-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

