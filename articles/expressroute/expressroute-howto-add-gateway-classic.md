---
title: "PowerShell을 사용하여 ExpressRoute용 VNet 게이트웨이 구성: classic: Azure | Microsoft Docs"
description: "Express 경로 구성을 위해 PowerShell을 사용하여 클래식 배포 모델 VNet에 대한 VNet 게이트웨이 구성"
documentationcenter: na
services: expressroute
author: charwen
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: 85ee0bc1-55be-4760-bfb4-34d9f2c96f30
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/21/2017
ms.author: charwen
ms.openlocfilehash: 195a38fa45f1c514a93980e777fb0d8238aa3f3f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-virtual-network-gateway-for-expressroute-using-powershell-classic"></a><span data-ttu-id="7a561-103">PowerShell을 사용하여 ExpressRoute용 가상 네트워크 게이트웨이 구성(클래식)</span><span class="sxs-lookup"><span data-stu-id="7a561-103">Configure a virtual network gateway for ExpressRoute using PowerShell (classic)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7a561-104">Resource Manager - PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a561-104">Resource Manager - PowerShell</span></span>](expressroute-howto-add-gateway-resource-manager.md)
> * [<span data-ttu-id="7a561-105">클래식 - PowerShell</span><span class="sxs-lookup"><span data-stu-id="7a561-105">Classic - PowerShell</span></span>](expressroute-howto-add-gateway-classic.md)
> * [<span data-ttu-id="7a561-106">비디오 - Azure Portal</span><span class="sxs-lookup"><span data-stu-id="7a561-106">Video - Azure Portal</span></span>](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-a-vpn-gateway-for-your-virtual-network)
> 
> 

<span data-ttu-id="7a561-107">이 문서에서는 기존 VNet에 대한 가상 네트워크(VNet) 게이트웨이를 추가하고, 크기를 조정하고, 제거하는 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="7a561-107">This article will walk you through the steps to add, resize, and remove a virtual network (VNet) gateway for a pre-existing VNet.</span></span> <span data-ttu-id="7a561-108">이 구성 단계는 특히 **클래식 배포 모델** 을 사용하여 만들었으며 Express 경로 구성에서 사용할 VNet을 위한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="7a561-108">The steps for this configuration are specifically for VNets that were created using the **classic deployment model** and that will be be used in an ExpressRoute configuration.</span></span> 

[!INCLUDE [expressroute-classic-end-include](../../includes/expressroute-classic-end-include.md)]

<span data-ttu-id="7a561-109">**Azure 배포 모델 정보**</span><span class="sxs-lookup"><span data-stu-id="7a561-109">**About Azure deployment models**</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

## <a name="before-beginning"></a><span data-ttu-id="7a561-110">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="7a561-110">Before beginning</span></span>
<span data-ttu-id="7a561-111">이 구성에 필요한 Azure PowerShell cmdlet을 설치했는지 확인합니다(1.0.2 이상).</span><span class="sxs-lookup"><span data-stu-id="7a561-111">Verify that you have installed the Azure PowerShell cmdlets needed for this configuration (1.0.2 or later).</span></span> <span data-ttu-id="7a561-112">Cmdlet을 설치하지 않은 경우 구성 단계를 시작하기 전에 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7a561-112">If you haven't installed the cmdlets, you'll need to do so before beginning the configuration steps.</span></span> <span data-ttu-id="7a561-113">Azure PowerShell 설치에 관한 자세한 내용은 [Azure PowerShell 설치 및 구성 방법](/powershell/azure/overview)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a561-113">For more information about installing Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [expressroute-gateway-classic-ps](../../includes/expressroute-gateway-classic-ps-include.md)]

## <a name="next-steps"></a><span data-ttu-id="7a561-114">다음 단계</span><span class="sxs-lookup"><span data-stu-id="7a561-114">Next steps</span></span>
<span data-ttu-id="7a561-115">VNet 게이트웨이를 만든 후 VNet을 Express 경로 회로에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7a561-115">After you have created the VNet gateway, you can link your VNet to an ExpressRoute circuit.</span></span> <span data-ttu-id="7a561-116">[가상 네트워크를 Express 경로 회로에 연결](expressroute-howto-linkvnet-classic.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7a561-116">See [Link a Virtual Network to an ExpressRoute circuit](expressroute-howto-linkvnet-classic.md).</span></span>

