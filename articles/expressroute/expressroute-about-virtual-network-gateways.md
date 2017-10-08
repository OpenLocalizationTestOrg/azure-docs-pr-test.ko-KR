---
title: "aaaAbout ExpressRoute 가상 네트워크 게이트웨이 | Microsoft Docs"
description: "ExpressRoute의 가상 네트워크 게이트웨이에 대해 알아봅니다."
services: expressroute
documentationcenter: na
author: cherylmc
manager: carmonm
editor: 
tags: azure-resource-manager, azure-service-management
ms.assetid: 7e0d9658-bc00-45b0-848f-f7a6da648635
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/05/2017
ms.author: cherylmc
ms.openlocfilehash: 4daf4f96b4fadb00683d8e536e51734853008c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="about-virtual-network-gateways-for-expressroute"></a>ExpressRoute에 대한 가상 네트워크 게이트웨이 정보
가상 네트워크 게이트웨이에 사용 되는 Azure 가상 네트워크와 온-프레미스 위치 사이의 네트워크 트래픽을 toosend 합니다. ExpressRoute 연결을 구성할 때 가상 네트워크 게이트웨이 및 가상 네트워크 게이트웨이 연결을 만들고 구성해야 합니다.

가상 네트워크 게이트웨이를 만들 때 몇 가지 설정을 지정합니다. 사이트 간 VPN 또는 express 경로도 트래픽에 대 한 hello 게이트웨이 사용할지 여부 필요한 hello 설정 중 하나를 지정 합니다. Hello 설정을 hello 리소스 관리자 배포 모델에는 '-GatewayType'.

개인 연결 네트워크 트래픽을 전송 하는 경우 'ExpressRoute' hello 게이트웨이 유형을 사용 합니다. 참조 된 tooas express 경로 게이트웨이 이기도합니다. 네트워크 트래픽을 암호화에서 전송 된 때 공용 인터넷 hello를 hello 게이트웨이 유형 'Vpn'를 사용 합니다. 참조 된 tooas VPN 게이트웨이입니다. 사이트 간, 지점 및 사이트 간, VNet 간 연결은 모두 VPN Gateway를 사용합니다.

각각의 가상 네트워크에는 게이트웨이 유형당 하나의 가상 네트워크 게이트웨이가 있을 수 있습니다. 예를 들어 -GatewayType Vpn을 사용하는 하나의 가상 네트워크 게이트웨이와 -GatewayType Express 경로를 사용하는 하나의 가상 네트워크 게이트웨이가 있을 수 있습니다. 이 문서는 hello ExpressRoute 가상 네트워크 게이트웨이에 중점을 둡니다.

## <a name="gwsku"></a>게이트웨이 SKU
[!INCLUDE [expressroute-gwsku-include](../../includes/expressroute-gwsku-include.md)]

원하는 tooupgrade 게이트웨이 tooa 더 강력 하는 경우 게이트웨이 SKU, 대부분의 경우 사용할 수 있습니다 hello ' 크기 조정 AzureRmVirtualNetworkGateway' PowerShell cmdlet. 이 기능은 업그레이드 tooStandard 및 HighPerformance Sku에 대 한 작동 됩니다. 그러나 tooupgrade toohello UltraPerformance SKU 해야 toorecreate hello 게이트웨이 합니다.

### <a name="aggthroughput"></a>게이트웨이 SKU에 의해 예상된 총 처리량
hello 다음 표에 hello 게이트웨이 유형 및 집계 처리량을 예상된 hello 있습니다. 이 테이블 tooboth hello 리소스 관리자 및 클래식 배포 모델을 적용합니다.

[!INCLUDE [expressroute-table-aggthroughput](../../includes/expressroute-table-aggtput-include.md)]

> [!IMPORTANT]
> Hello 수가 트래픽 흐름 hello 응용 프로그램 열립니다 및 응용 프로그램 처리량 hello 종단 간 대기 시간 등의 여러 요인에 따라 다릅니다. hello 숫자 hello 테이블 나타내는 hello 상한 hello 응용 프로그램 theorectically 수 있는 이상적인 환경에서 달성 합니다. 
> 
>

## <a name="resources"></a>REST API 및 PowerShell cmdlet
추가 기술 리소스 및 가상 네트워크 게이트웨이 구성에 대 한 REST Api 및 PowerShell cmdlet을 사용 하는 경우 특정 구문 요구 사항에 대 한 hello 다음 페이지를 참조:

| **클래식** | **리소스 관리자** |
| --- | --- |
| [PowerShell](https://msdn.microsoft.com/library/mt270335.aspx) |[PowerShell](https://msdn.microsoft.com/library/mt163510.aspx) |
| [REST API](https://msdn.microsoft.com/library/jj154113.aspx) |[REST API](https://msdn.microsoft.com/library/mt163859.aspx) |

## <a name="next-steps"></a>다음 단계
사용 가능한 연결 구성에 대한 자세한 내용은 [ExpressRoute 개요](expressroute-introduction.md) 를 참조하세요. 

