---
title: "ExpressRoute용 VNet에 가상 네트워크 게이트웨이 추가: PowerShell: Azure | Microsoft Docs"
description: "이 문서에서는 ExpressRoute에 대해 이미 만들어진 Resource Manager VNet에 VNet 게이트웨이를 추가하는 과정을 안내합니다."
documentationcenter: na
services: expressroute
author: charwen
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 63e0bd60-abad-4963-8e27-3aa973e0d968
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/17/2017
ms.author: charwen
ms.openlocfilehash: 3aeddd03e0be548933775164ae790ba208fc13ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="0aa97-103">PowerShell을 사용하여 ExpressRoute에 대한 가상 네트워크 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="0aa97-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0aa97-104">Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0aa97-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="0aa97-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="0aa97-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="0aa97-106">클래식 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="0aa97-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="0aa97-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="0aa97-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="0aa97-108">이 문서에서는 기존 VNet에 대한 가상 네트워크(VNet) 게이트웨이를 추가, 제거하고 크기를 조정하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="0aa97-108">This article walks you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="0aa97-109">이 구성에서 수행하는 단계는 Resource Manager 배포 모델을 사용하여 만든 VNet(ExpressRoute 구성에서 사용됨)에만 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="0aa97-109">The steps for this configuration are specifically for VNets that were created using the Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="0aa97-110">가상 네트워크 게이트웨이 및 ExpressRoute의 게이트웨이 구성 설정에 대한 자세한 내용은 [ExpressRoute에 대한 가상 네트워크 게이트웨이 정보](expressroute-about-virtual-network-gateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0aa97-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="0aa97-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="0aa97-111">Before beginning</span></span>
<span data-ttu-id="0aa97-112">최신 Azure PowerShell cmdlet를 설치했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0aa97-112">Verify that you have installed the latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="0aa97-113">cmdlet을 설치하지 않은 경우 구성 단계를 시작하기 전에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0aa97-113">If you haven't installed the latest cmdlets, you need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="0aa97-114">자세한 내용은 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0aa97-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="0aa97-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0aa97-115">Next steps</span></span>
<span data-ttu-id="0aa97-116">VNet 게이트웨이를 만든 후 VNet을 Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0aa97-116">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="0aa97-117">[가상 네트워크를 Express 경로 회로에 연결](expressroute-howto-linkvnet-arm.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0aa97-117">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

