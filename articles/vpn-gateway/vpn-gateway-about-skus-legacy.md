---
title: "Azure 가상 네트워크 게이트웨이 Sku aaaLegacy | Microsoft Docs"
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
ms.openlocfilehash: 710417581423d2fbc62827cab7949f2e137c5996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a><span data-ttu-id="82cbc-103">가상 네트워크 게이트웨이 SKU(레거시 SKU) 사용</span><span class="sxs-lookup"><span data-stu-id="82cbc-103">Working with virtual network gateway SKUs (legacy SKUs)</span></span>

<span data-ttu-id="82cbc-104">이 문서는 hello 레거시 (이전) 가상 네트워크 게이트웨이 Sku에 대 한 정보를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-104">This article contains information about hello legacy (old) virtual network gateway SKUs.</span></span> <span data-ttu-id="82cbc-105">hello 레거시 Sku 이미 생성 된 VPN 게이트웨이에 대 한 배포 모델 모두에서 계속 작동 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-105">hello legacy SKUs still work in both deployment models for VPN gateways that have already been created.</span></span> <span data-ttu-id="82cbc-106">클래식 VPN 게이트웨이 toouse 계속 기존 게이트웨이 및 새 게이트웨이에 대 한 레거시 Sku hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-106">Classic VPN gateways continue toouse hello legacy SKUs, both for existing gateways, and for new gateways.</span></span> <span data-ttu-id="82cbc-107">새 리소스 관리자 VPN 게이트웨이 만들 때는 hello 새 게이트웨이 Sku를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-107">When creating new Resource Manager VPN gateways, use hello new gateway SKUs.</span></span> <span data-ttu-id="82cbc-108">Hello에 대 한 정보에 대 한 새 Sku 참조 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-108">For information about hello new SKUs, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>

## <span data-ttu-id="82cbc-109"><a name="gwsku"></a>게이트웨이 SKU</span><span class="sxs-lookup"><span data-stu-id="82cbc-109"><a name="gwsku"></a>Gateway SKUs</span></span>

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <span data-ttu-id="82cbc-110"><a name="agg"></a>SKU 기준으로 예상된 총 처리량</span><span class="sxs-lookup"><span data-stu-id="82cbc-110"><a name="agg"></a>Estimated aggregate throughput by SKU</span></span>

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <span data-ttu-id="82cbc-111"><a name="config"></a>SKU와 VPN 형식별 지원되는 구성</span><span class="sxs-lookup"><span data-stu-id="82cbc-111"><a name="config"></a>Supported configurations by SKU and VPN type</span></span>

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <span data-ttu-id="82cbc-112"><a name="resize"></a>게이트웨이 크기 조정(게이트웨이 SKU 변경)</span><span class="sxs-lookup"><span data-stu-id="82cbc-112"><a name="resize"></a>Resize a gateway (change a gateway SKU)</span></span>

<span data-ttu-id="82cbc-113">게이트웨이 SKU hello 내에서 크기를 조정할 수 같은 SKU 제품군입니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-113">You can resize a gateway SKU within hello same SKU family.</span></span> <span data-ttu-id="82cbc-114">예를 들어 표준 SKU를 설정한 경우 tooa HighPerformance SKU 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-114">For example, if you have a Standard SKU, you can resize tooa HighPerformance SKU.</span></span> <span data-ttu-id="82cbc-115">VPN의 크기를 조정할 수 없는 이전 Sku hello와 새 SKU 제품군 hello 간 게이트웨이 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-115">You can't resize your VPN gateways between hello old SKUs and hello new SKU families.</span></span> <span data-ttu-id="82cbc-116">예를 들어 표준 SKU tooa VpnGw2 SKU에서에서 이동할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-116">For example, you can't go from a Standard SKU tooa VpnGw2 SKU.</span></span> 

<span data-ttu-id="82cbc-117">tooresize hello 클래식 배포 모델에서 다음 명령을 사용 하 여 hello에 대 한 게이트웨이 SKU:</span><span class="sxs-lookup"><span data-stu-id="82cbc-117">tooresize a gateway SKU for hello classic deployment model, use hello following command:</span></span>

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

<span data-ttu-id="82cbc-118">hello 리소스 관리자 배포 모델에 대 한 게이트웨이 SKU tooresize hello 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-118">tooresize a gateway SKU for hello Resource Manager deployment model, use hello following command:</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <span data-ttu-id="82cbc-119"><a name="migrate"></a>Toohello 새 게이트웨이 Sku 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="82cbc-119"><a name="migrate"></a>Migrate toohello new gateway SKUs</span></span>

<span data-ttu-id="82cbc-120">Hello 리소스 관리자 배포 모델을 사용 하는 경우에 toohello 새 게이트웨이 SKU를 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-120">If you are working with hello Resource Manager deployment model, you can migrate toohello new gateway SKUS.</span></span> <span data-ttu-id="82cbc-121">Toohello를 마이그레이션할 수 없습니다 hello 클래식 배포 모델을 사용 하는 경우 새 Sku toouse 계속 해야 하 고 hello 레거시 Sku입니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-121">If you are working with hello classic deployment model, you can't migrate toohello new SKUs and must instead continue toouse hello legacy SKUs.</span></span>

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a><span data-ttu-id="82cbc-122">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82cbc-122">Next steps</span></span>

<span data-ttu-id="82cbc-123">새 게이트웨이 Sku hello에 대 한 자세한 내용은 참조 하십시오. [게이트웨이 Sku](vpn-gateway-about-vpngateways.md#gwsku)합니다.</span><span class="sxs-lookup"><span data-stu-id="82cbc-123">For more information about hello new Gateway SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

<span data-ttu-id="82cbc-124">구성 설정에 대한 자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82cbc-124">For more information about configuration settings, see [About VPN Gateway configuration settings](vpn-gateway-about-vpn-gateway-settings.md).</span></span>