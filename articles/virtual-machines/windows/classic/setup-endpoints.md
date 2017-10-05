---
title: "클래식 Windows VM에서 끝점 설정 | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터와 통신을 허용하도록 Azure 클래식 포털에서 Windows VM에 대한 끝점을 설정하는 방법에 대해 알아봅니다."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 8afc21c2-d3fb-43a3-acce-aa06be448bb6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: cynthn
ms.openlocfilehash: 60861819a7e437bb715b14c0e8eaf74f13b33ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-set-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="c6786-103">Azure에서 클래식 Windows 가상 컴퓨터에 끝점을 설정하는 방법</span><span class="sxs-lookup"><span data-stu-id="c6786-103">How to set up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="c6786-104">클래식 배포 모델을 사용하여 Azure에서 만든 모든 Windows 가상 컴퓨터는 개인 네트워크 채널을 통해 동일한 클라우드 서비스 또는 가상 네트워크에 있는 다른 가상 컴퓨터와 자동으로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6786-104">All Windows virtual machines that you create in Azure using the classic deployment model can automatically communicate over a private network channel with other virtual machines in the same cloud service or virtual network.</span></span> <span data-ttu-id="c6786-105">그러나 인터넷이나 다른 가상 네트워크의 컴퓨터가 가상 컴퓨터로 인바운드 네트워크 트래픽을 전달하려면 끝점이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c6786-105">However, computers on the Internet or other virtual networks require endpoints to direct the inbound network traffic to a virtual machine.</span></span> <span data-ttu-id="c6786-106">이 문서는 [Linux 가상 컴퓨터](../../linux/classic/setup-endpoints.md)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c6786-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c6786-107">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6786-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c6786-108">이 문서에서는 클래식 배포 모델 사용에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="c6786-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c6786-109">새로운 배포는 대부분 리소스 관리자 모델을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c6786-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="c6786-110">**Resource Manager** 배포 모델에서는 **NSG(네트워크 보안 그룹)**를 사용하여 끝점을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="c6786-110">In the **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="c6786-111">자세한 내용은 [Azure Portal을 사용하여 VM에 대한 외부 액세스 허용](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6786-111">For more information, see [Allow external access to your VM using the Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c6786-112">Azure Portal에서 Windows 가상 컴퓨터를 만들 때 원격 데스크톱, Windows PowerShell 원격 등에 대한 일반적인 끝점은 일반적으로 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="c6786-112">When you create a Windows virtual machine in the Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="c6786-113">가상 컴퓨터를 만드는 동안 또는 가상 컴퓨터를 만든 후 필요에 따라 추가 끝점을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c6786-113">You can configure additional endpoints while creating the virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="c6786-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c6786-114">Next steps</span></span>
* <span data-ttu-id="c6786-115">Azure PowerShell cmdlet을 사용하여 VM 끝점을 설정하려면 [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6786-115">To use an Azure PowerShell cmdlet to set up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="c6786-116">Azure PowerShell cmdlet을 사용하여 끝점에서 ACL을 관리하려면 [PowerShell을 사용하여 끝점에 대한 ACL(액세스 제어 목록) 관리](../../../virtual-network/virtual-networks-acl-powershell.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c6786-116">To use an Azure PowerShell cmdlet to manage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="c6786-117">리소스 관리자 배포 모델에서 가상 컴퓨터를 만들면, Azure PowerShell을 사용하여 VM에 대한 트래픽을 제어하는 [네트워크 보안 그룹을 만들 수 있습니다](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) .</span><span class="sxs-lookup"><span data-stu-id="c6786-117">If you created a virtual machine in the Resource Manager deployment model, you can use Azure PowerShell to [create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) to control traffic to the VM.</span></span>
