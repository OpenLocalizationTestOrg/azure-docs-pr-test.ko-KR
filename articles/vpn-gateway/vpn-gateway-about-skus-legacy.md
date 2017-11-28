---
title: "레거시 Azure Virtual Network 게이트웨이 SKU | Microsoft Docs"
description: "이전 가상 네트워크 게이트웨이 SKU입니다."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/01/2017
ms.author: cherylmc
ms.openlocfilehash: 3b2126b1ecd1613950bbf311ae08fafd4af0d51f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="b45f9-103">가상 네트워크 게이트웨이 SKU(레거시 SKU) 사용</span><span class="sxs-lookup"><span data-stu-id="b45f9-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="b45f9-104">이 문서에는 레거시(이전) 가상 네트워크 게이트웨이 SKU에 대한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-104">This article contains information about the legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="b45f9-105">레거시 SKU는 이미 작성된 VPN Gateway의 두 배포 모델에서 모두 계속 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-105">The legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="b45f9-106">클래식 VPN Gateway는 레거시 SKU를 계속 사용합니다(기존 게이트웨이와 새 게이트웨이 둘 다를 위해).</span><span class="sxs-lookup"><span data-stu-id="b45f9-106">Classic VPN gateways continue to use the legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="b45f9-107">새 Resource Manager VPN Gateway를 만들 때는 새 게이트웨이 SKU를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-107">When creating new Resource Manager VPN gateways, use the new gateway SKUs.</span></span> <span data-ttu-id="b45f9-108">새 SKU에 대한 자세한 내용은 [VPN Gateway 정보](vpn-gateway-about-vpngateways.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b45f9-108">For information about the new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="b45f9-109"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="b45f9-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="b45f9-110"><a name="agg"></a>SKU 기준으로 예상된 총 처리량</span><span class="sxs-lookup"><span data-stu-id="b45f9-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="b45f9-111"><a name="config"></a>SKU와 VPN 형식별 지원되는 구성</span><span class="sxs-lookup"><span data-stu-id="b45f9-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="b45f9-112"><a name="resize"></a>게이트웨이 크기 조정(게이트웨이 SKU 변경)</span><span class="sxs-lookup"><span data-stu-id="b45f9-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="b45f9-113">동일한 SKU 제품군 내에서 게이트웨이 SKU 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-113">You can resize a gateway SKU within the same SKU family.</span></span> <span data-ttu-id="b45f9-114">예를 들어 Standard SKU는 HighPerformance SKU로 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-114">For example, if you have a Standard SKU, you can resize to a HighPerformance SKU.</span></span> <span data-ttu-id="b45f9-115">이전 SKU와 새 SKU 제품군 간에 VPN Gateway의 크기를 조정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-115">You can't resize your VPN gateways between the old SKUs and the new SKU families.</span></span> <span data-ttu-id="b45f9-116">예를 들어 Standard SKU에서 VpnGw2 SKU로 크기를 조정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-116">For example, you can't go from a Standard SKU to a VpnGw2 SKU.</span></span> 

<span data-ttu-id="b45f9-117">클래식 배포 모델의 게이트웨이 SKU 크기를 조정하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-117">To resize a gateway SKU for the classic deployment model, use the following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="b45f9-118">Resource Manager 배포 모델의 게이트웨이 SKU 크기를 조정하려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-118">To resize a gateway SKU for the Resource Manager deployment model, use the following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="b45f9-119"><a name="migrate"></a>새 게이트웨이 SKU로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="b45f9-119"><a name="migrate"></a>Migrate to the new gateway SKUs</span></span>

<span data-ttu-id="b45f9-120">Resource Manager 배포 모델을 사용하는 경우 새 게이트웨이 SKU로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-120">If you are working with the Resource Manager deployment model, you can migrate to the new gateway SKUS.</span></span> <span data-ttu-id="b45f9-121">클래식 배포 모델을 사용하는 경우에는 새 SKU로 마이그레이션할 수 없으며 대신 레거시 SKU를 계속 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b45f9-121">If you are working with the classic deployment model, you can't migrate to the new SKUs and must instead continue to use the legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b45f9-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="b45f9-122">Next steps</span></span>

<span data-ttu-id="b45f9-123">새 게이트웨이 SKU에 대한 자세한 내용은 [게이트웨이 SKU](vpn-gateway-about-vpngateways.md#gwsku)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b45f9-123">For more information about the new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="b45f9-124">구성 설정에 대한 자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b45f9-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>