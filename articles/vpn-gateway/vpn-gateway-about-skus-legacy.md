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
# <a name="working-with-virtual-network-gateway-skus-legacy-skus"></a>가상 네트워크 게이트웨이 SKU(레거시 SKU) 사용

이 문서는 hello 레거시 (이전) 가상 네트워크 게이트웨이 Sku에 대 한 정보를 포함합니다. hello 레거시 Sku 이미 생성 된 VPN 게이트웨이에 대 한 배포 모델 모두에서 계속 작동 합니다. 클래식 VPN 게이트웨이 toouse 계속 기존 게이트웨이 및 새 게이트웨이에 대 한 레거시 Sku hello 합니다. 새 리소스 관리자 VPN 게이트웨이 만들 때는 hello 새 게이트웨이 Sku를 사용 합니다. Hello에 대 한 정보에 대 한 새 Sku 참조 [에 대 한 VPN 게이트웨이](vpn-gateway-about-vpngateways.md)합니다.

## <a name="gwsku"></a>게이트웨이 SKU

[!INCLUDE [Legacy gateway SKUs](../../includes/vpn-gateway-gwsku-legacy-include.md)]

## <a name="agg"></a>SKU 기준으로 예상된 총 처리량

[!INCLUDE [Aggregated throughput by legacy SKU](../../includes/vpn-gateway-table-gwtype-legacy-aggtput-include.md)]

## <a name="config"></a>SKU와 VPN 형식별 지원되는 구성

[!INCLUDE [Table requirements for old SKUs](../../includes/vpn-gateway-table-requirements-legacy-sku-include.md)]

## <a name="resize"></a>게이트웨이 크기 조정(게이트웨이 SKU 변경)

게이트웨이 SKU hello 내에서 크기를 조정할 수 같은 SKU 제품군입니다. 예를 들어 표준 SKU를 설정한 경우 tooa HighPerformance SKU 크기를 조정할 수 있습니다. VPN의 크기를 조정할 수 없는 이전 Sku hello와 새 SKU 제품군 hello 간 게이트웨이 합니다. 예를 들어 표준 SKU tooa VpnGw2 SKU에서에서 이동할 수 없습니다. 

tooresize hello 클래식 배포 모델에서 다음 명령을 사용 하 여 hello에 대 한 게이트웨이 SKU:

```powershell
Resize-AzureVirtualNetworkGateway -GatewayId <Gateway ID> -GatewaySKU HighPerformance
```

hello 리소스 관리자 배포 모델에 대 한 게이트웨이 SKU tooresize hello 다음 명령을 사용 합니다.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku HighPerformance
```

## <a name="migrate"></a>Toohello 새 게이트웨이 Sku 마이그레이션

Hello 리소스 관리자 배포 모델을 사용 하는 경우에 toohello 새 게이트웨이 SKU를 마이그레이션할 수 있습니다. Toohello를 마이그레이션할 수 없습니다 hello 클래식 배포 모델을 사용 하는 경우 새 Sku toouse 계속 해야 하 고 hello 레거시 Sku입니다.

[!INCLUDE [Migrate SKU](../../includes/vpn-gateway-migrate-legacy-sku-include.md)]

## <a name="next-steps"></a>다음 단계

새 게이트웨이 Sku hello에 대 한 자세한 내용은 참조 하십시오. [게이트웨이 Sku](vpn-gateway-about-vpngateways.md#gwsku)합니다.

구성 설정에 대한 자세한 내용은 [VPN Gateway 구성 설정 정보](vpn-gateway-about-vpn-gateway-settings.md)를 참조하세요.