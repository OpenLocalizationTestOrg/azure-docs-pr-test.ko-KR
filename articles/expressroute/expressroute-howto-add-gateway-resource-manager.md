---
title: "ExpressRoute에 대 한 가상 네트워크 게이트웨이 tooa VNet 추가: PowerShell: Azure | Microsoft Docs"
description: "이 문서에서는 이미 ExpressRoute에 대 한 리소스 관리자 VNet을 만든 VNet 게이트웨이 tooan를 추가 하는 과정을 안내 합니다."
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
ms.openlocfilehash: 8983430b426ad7c4af766294fa16427c5e9df5c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell"></a><span data-ttu-id="95989-103">PowerShell을 사용하여 ExpressRoute에 대한 가상 네트워크 게이트웨이 구성</span><span class="sxs-lookup"><span data-stu-id="95989-103">Configure a virtual network gateway for ExpressRoute using PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95989-104">Resource Manager - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="95989-104">Resource Manager - Azure portal</span></span>](expressroute-howto-add-gateway-portal-resource-manager.md)
> * [<span data-ttu-id="95989-105">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="95989-105">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="95989-106">클래식 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="95989-106">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="95989-107">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="95989-107">Video - Azure portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="95989-108">이 문서 단계별로 hello 단계 tooadd, 크기 조정 및 기존 VNet에 대 한 가상 네트워크 (VNet) 게이트웨이 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="95989-108">This article walks you through hello steps tooadd, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="95989-109">이 구성에 대 한 hello 단계 ExpressRoute 구성에 사용할 hello 리소스 관리자 배포 모델을 사용 하 여 만든 Vnet에 대 한 구체적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="95989-109">hello steps for this configuration are specifically for VNets that were created using hello Resource Manager deployment model that will be used in an ExpressRoute configuration.</span></span> <span data-ttu-id="95989-110">가상 네트워크 게이트웨이 및 ExpressRoute의 게이트웨이 구성 설정에 대한 자세한 내용은 [ExpressRoute에 대한 가상 네트워크 게이트웨이 정보](expressroute-about-virtual-network-gateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95989-110">For more information about virtual network gateways and gateway configuration settings for ExpressRoute, see [About virtual network gateways for ExpressRoute](expressroute-about-virtual-network-gateways.md).</span></span> 


## <a name="before-beginning"></a><span data-ttu-id="95989-111">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="95989-111">Before beginning</span></span>
<span data-ttu-id="95989-112">Hello 최신 Azure PowerShell cmdlet을 설치 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95989-112">Verify that you have installed hello latest Azure PowerShell cmdlets.</span></span> <span data-ttu-id="95989-113">Toodo hello 최신 cmdlet를 설치 하지 않은 경우 해야 하므로 hello 구성 단계를 시작 하기 전에.</span><span class="sxs-lookup"><span data-stu-id="95989-113">If you haven't installed hello latest cmdlets, you need toodo so before beginning hello configuration steps.</span></span> <span data-ttu-id="95989-114">자세한 내용은 [Azure PowerShell 설치 및 구성](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95989-114">For more information, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-rm-ps](../../includes/expressroute-gateway-rm-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="95989-115">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95989-115">Next steps</span></span>
<span data-ttu-id="95989-116">Hello VNet 게이트웨이 만든 후에 VNet tooan ExpressRoute 회로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95989-116">After you have created hello VNet gateway, you can link your VNet tooan ExpressRoute circuit.</span></span> <span data-ttu-id="95989-117">참조 [가상 네트워크 tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95989-117">See [Link a Virtual Network tooan ExpressRoute circuit](expressroute-howto-linkvnet-arm.md).</span></span>

