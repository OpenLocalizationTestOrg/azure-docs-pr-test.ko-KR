---
title: "Azure Portal에서 Windows VM에 대한 FQDN 만들기 | Microsoft Docs"
description: "Azure Portal에서 가상 컴퓨터를 기반으로 한 Resource Manager에 대한 정규화된 도메인 이름 또는 FQDN을 만드는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: a2ae5887-76df-485e-ae19-0efd96df8600
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2d5a555cd873222efcdb29e8eb3aaf128a24414b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-windows-vm"></a><span data-ttu-id="d9370-103">Windows VM용 Azure Portal에서 정규화된 도메인 이름 만들기</span><span class="sxs-lookup"><span data-stu-id="d9370-103">Create a fully qualified domain name in the Azure portal for a Windows VM</span></span>

<span data-ttu-id="d9370-104">[Azure Portal](https://portal.azure.com)에서 VM(가상 컴퓨터)을 만들 때, 가상 컴퓨터의 공용 IP 리소스가 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-104">When you create a virtual machine (VM) in the [Azure portal](https://portal.azure.com), a public IP resource for the virtual machine is automatically created.</span></span> <span data-ttu-id="d9370-105">이 IP 주소를 사용하여 VM에 원격으로 액세스합니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-105">You use this IP address to remotely access the VM.</span></span> <span data-ttu-id="d9370-106">포털에서 [정규화된 도메인 이름](https://en.wikipedia.org/wiki/Fully_qualified_domain_name) 또는 FQDN을 만들지는 않지만 VM을 만들면 이름을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-106">Although the portal does not create a [fully qualified domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name), or FQDN, you can create one once the VM is created.</span></span> <span data-ttu-id="d9370-107">이 문서에서는 DNS 이름 또는 FQDN을 만드는 단계를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-107">This article demonstrates the steps to create a DNS name or FQDN.</span></span>

## <a name="create-a-fqdn"></a><span data-ttu-id="d9370-108">FQDN 만들기</span><span class="sxs-lookup"><span data-stu-id="d9370-108">Create a FQDN</span></span>
<span data-ttu-id="d9370-109">이 문서에서는 사용자가 VM을 이미 만들었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-109">This article assumes that you have already created a VM.</span></span> <span data-ttu-id="d9370-110">필요한 경우 [포털에서](quick-create-portal.md) 또는 [Azure PowerShell을 사용하여](quick-create-powershell.md) VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-110">If needed, you can [create a VM in the portal](quick-create-portal.md) or [with Azure PowerShell](quick-create-powershell.md).</span></span> <span data-ttu-id="d9370-111">VM이 실행되면 다음 단계를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-111">Follow these steps once your VM is up and running:</span></span>

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

<span data-ttu-id="d9370-112">이제 RDP(원격 데스크톱 프로토콜)의 경우처럼 이 DNS 이름을 사용하여 원격으로 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-112">You can now connect remotely to the VM using this DNS name such as for Remote Desktop Protocol (RDP).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9370-113">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d9370-113">Next steps</span></span>
<span data-ttu-id="d9370-114">VM에 공용 IP 및 DNS 이름을 지정했으므로 IIS, SQL, SharePoint 등의 공용 응용 프로그램 프레임워크 또는 서비스를 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-114">Now that your VM has a public IP and DNS name, you can deploy common application frameworks or services such as IIS, SQL, or SharePoint.</span></span>

<span data-ttu-id="d9370-115">또한 Azure 배포 구축에 대한 팁을 보려면 [Resource Manager 사용](../../azure-resource-manager/resource-group-overview.md)에 대해 자세히 읽어볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d9370-115">You can also read more about [using Resource Manager](../../azure-resource-manager/resource-group-overview.md) for tips on building your Azure deployments.</span></span>

