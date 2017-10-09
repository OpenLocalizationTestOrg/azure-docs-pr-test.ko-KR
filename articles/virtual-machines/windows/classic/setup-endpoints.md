---
title: "클래식 Windows VM에서 끝점을 aaaSet | Microsoft Docs"
description: "Azure에서 Windows 가상 컴퓨터를 사용 하 여 hello Azure 클래식 포털 tooallow 통신에에서 Windows VM에 대 한 끝점을 tooset에 알아봅니다."
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
ms.openlocfilehash: e817076f16d3a245a8d19add7b2f2cf5e3baa17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooset-up-endpoints-on-a-classic-windows-virtual-machine-in-azure"></a><span data-ttu-id="5f228-103">어떻게 tooset azure에서 클래식 Windows 가상 컴퓨터 끝점을</span><span class="sxs-lookup"><span data-stu-id="5f228-103">How tooset up endpoints on a classic Windows virtual machine in Azure</span></span>
<span data-ttu-id="5f228-104">모든 Windows hello 클래식 배포 모델을 사용 하 여 Azure에서 만드는 가상 컴퓨터에 다른 가상 컴퓨터와 개인 네트워크 채널을 통해 자동으로 통신할 수에 동일한 클라우드 서비스 또는 가상 네트워크 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-104">All Windows virtual machines that you create in Azure using hello classic deployment model can automatically communicate over a private network channel with other virtual machines in hello same cloud service or virtual network.</span></span> <span data-ttu-id="5f228-105">그러나 hello 인터넷 또는 다른 가상 네트워크에 있는 컴퓨터에 끝점 toodirect hello 인바운드 네트워크 트래픽을 tooa 가상 컴퓨터가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-105">However, computers on hello Internet or other virtual networks require endpoints toodirect hello inbound network traffic tooa virtual machine.</span></span> <span data-ttu-id="5f228-106">이 문서는 [Linux 가상 컴퓨터](../../linux/classic/setup-endpoints.md)에도 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-106">This article is also available for [Linux virtual machines](../../linux/classic/setup-endpoints.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f228-107">Azure에는 리소스를 만들고 작업하기 위한 [리소스 관리자 및 클래식](../../../resource-manager-deployment-model.md)라는 두 가지 배포 모델이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="5f228-108">이 문서에서는 hello 클래식 배포 모델을 사용 하 여 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-108">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="5f228-109">대부분의 새로운 배포 hello 리소스 관리자 모델을 사용 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-109">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="5f228-110">Hello에 **리소스 관리자** 배포 모델을 사용 하 여 끝점이 구성 **(Nsg) 네트워크 보안 그룹**합니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-110">In hello **Resource Manager** deployment model, endpoints are configured using **Network Security Groups (NSGs)**.</span></span> <span data-ttu-id="5f228-111">자세한 내용은 참조 [Azure 포털 hello 허용 외부 액세스 tooyour 사용 하 여 VM](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-111">For more information, see [Allow external access tooyour VM using hello Azure portal](../nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="5f228-112">Hello Azure 포털에서에서 Windows 가상 컴퓨터를 만들 때 원격 데스크톱 및 Windows PowerShell 원격에 대 한 것과 같은 일반적인 끝점 일반적으로 사용자에 대 한 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-112">When you create a Windows virtual machine in hello Azure portal, common endpoints like those for Remote Desktop and Windows PowerShell Remoting are typically created for you automatically.</span></span> <span data-ttu-id="5f228-113">Hello 가상 컴퓨터를 만드는 동안 또는 나중에 필요에 따라 추가 끝점을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-113">You can configure additional endpoints while creating hello virtual machine or afterwards as needed.</span></span>

[!INCLUDE [virtual-machines-common-classic-setup-endpoints](../../../../includes/virtual-machines-common-classic-setup-endpoints.md)]

## <a name="next-steps"></a><span data-ttu-id="5f228-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="5f228-114">Next steps</span></span>
* <span data-ttu-id="5f228-115">Azure PowerShell cmdlet tooset VM 끝점을 toouse 참조 [Add-azureendpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-115">toouse an Azure PowerShell cmdlet tooset up a VM endpoint, see [Add-AzureEndpoint](https://msdn.microsoft.com/library/azure/dn495300.aspx).</span></span>
* <span data-ttu-id="5f228-116">Azure PowerShell cmdlet toomanage는 끝점에 대 한 ACL toouse 참조 [관리 액세스 제어 목록 (Acl 끝점에 대 한 PowerShell을 사용 하 여)](../../../virtual-network/virtual-networks-acl-powershell.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-116">toouse an Azure PowerShell cmdlet toomanage an ACL on an endpoint, see [Managing access control lists (ACLs) for endpoints by using PowerShell](../../../virtual-network/virtual-networks-acl-powershell.md).</span></span>
* <span data-ttu-id="5f228-117">Hello 리소스 관리자 배포 모델에서 가상 컴퓨터를 만든 경우 Azure PowerShell을도 사용할 수 있습니다[네트워크 보안 그룹을 만들고](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol 트래픽 toohello VM입니다.</span><span class="sxs-lookup"><span data-stu-id="5f228-117">If you created a virtual machine in hello Resource Manager deployment model, you can use Azure PowerShell too[create network security groups](../../../virtual-network/virtual-networks-create-nsg-arm-ps.md) toocontrol traffic toohello VM.</span></span>
