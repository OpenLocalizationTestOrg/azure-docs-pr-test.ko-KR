---
title: "Azure VPN 게이트웨이 사용한 BGP의 aaaOverview | Microsoft Docs"
description: "이 문서는 Azure VPN Gateway와 BGP에 대한 개요를 제공합니다."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: f8c3985c-c128-4f34-835c-0e88742bf36e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/12/2017
ms.author: yushwang
ms.openlocfilehash: ced3f77ecd791c84fb72b96447e839be3bf94846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-bgp-with-azure-vpn-gateways"></a>Azure VPN Gateway에서의 BGP 개요
이 문서에서는 Azure VPN Gateway에서의 BGP(경계 게이트웨이 프로토콜) 지원에 대한 개요를 제공합니다.

BGP는 hello 표준 라우팅 프로토콜 hello 인터넷 tooexchange 라우팅과 연결 가능성 정보 두 개 이상의 네트워크 사이에서 일반적으로 사용 합니다. 때 Azure 가상 네트워크의 hello 컨텍스트에서 사용 되는, BGP hello Azure VPN 게이트웨이 및 BGP 피어를 호출 하 여 온-프레미스 VPN 장치를 사용 하거나 tooexchange 이웃 "같은 경로" 하는 것에 대 한 연결 가능성이 hello 가용성에 두 게이트웨이 알려줄 것 hello 게이트웨이 또는 라우터로 관련 된 통해 toogo 접두사를 추가 합니다. BGP 경로 BGP 게이트웨이 한 BGP 피어 tooall에서 학습을 전파 하 여 여러 네트워크 간에 전송 라우팅과 활성화할 수도 다른 BGP 피어입니다. 

## <a name="why-use-bgp"></a>BGP를 사용하는 이유
BGP는 선택적 기능으로, Azure 경로 기반 VPN Gateway와 함께 사용할 수 있습니다. 또한 온-프레미스 VPN 장치 hello 기능을 활성화 하기 전에 BGP를 지원 해야 합니다. Toouse Azure VPN 게이트웨이 및 BGP 없이 온-프레미스 VPN 장치를 계속할 수 있습니다. Hello (BGP) 없이 고정 경로 사용 하 여 해당 하는 *비교* 네트워크와 Azure 간의 BGP를 사용 동적 라우팅을 사용 합니다.

BGP에는 다음과 같이 몇 가지 장점과 새로운 기능이 있습니다.

### <a name="support-automatic-and-flexible-prefix-updates"></a>자동 및 유연한 접두사 업데이트 지원
BGP를 사용 하면 최소 접두사 tooa 특정 BGP 피어 toodeclare hello IPsec S2S VPN 터널을 통해 됩니다. 호스트 접두사로 작을 수 (/ 32) hello 온-프레미스 VPN 장치의 BGP 피어 IP 주소입니다. 온-프레미스 Azure 가상 네트워크 tooaccess tooadvertise tooAzure tooallow 원하는 네트워크 접두사를 제어할 수 있습니다.

또한 대형 비공개 IP 주소 공간(예: 10.0.0.0/8)과 같은 일부 VNet 주소 접두어를 포함하는 더 큰 접두어를 제시할 수도 있습니다. Note 있지만 hello 접두사 VNet 접두사 중 하나로 인해 같을 수 없습니다. 이러한 경로 동일한 tooyour VNet 접두사가 거부 됩니다.

### <a name="support-multiple-tunnels-between-a-vnet-and-an-on-premises-site-with-automatic-failover-based-on-bgp"></a>BGP를 기준으로 자동 장애 조치가 있는 VNet과 온-프레미스 사이트 간 여러 터널 지원
Hello에서 Azure VNet 및 온-프레미스 VPN 장치 간의 다중 연결을 설정할 수 있습니다 있습니다 동일한 위치입니다. 이 기능은 hello 활성-활성 구성에서 두 네트워크 간에 여러 터널 (경로)를 제공합니다. Hello 터널 중 하나는 연결이 끊어졌기 hello 해당 경로 BGP를 통해 제거 됩니다 및 hello 트래픽 toohello 나머지 터널을 자동으로 이동 합니다.

다음 다이어그램 hello이 항상 사용 가능한 설치의 간단한 예를 보여 줍니다.

![여러 개의 활성 경로](./media/vpn-gateway-bgp-overview/multiple-active-tunnels.png)

### <a name="support-transit-routing-between-your-on-premises-networks-and-multiple-azure-vnets"></a>온-프레미스 네트워크와 여러 Azure VNet 간 전송 라우팅 지원
BGP 여러 게이트웨이 toolearn 있으며 특정 직접 또는 간접적으로 연결 되어 있는지 여부를 서로 다른 네트워크에서 접두사를 전파 합니다. 따라서 온-프레미스 사이트 간 또는 여러 Azure 가상 네트워크 간의 Azure VPN Gateway를 통한 전송  라우팅이 가능합니다.

hello 다음 다이어그램의 예가 나와 hello Microsoft 네트워크 내에서 Azure VPN 게이트웨이 통해 hello 두 온-프레미스 네트워크 간에 트래픽을 전송 수 있는 여러 경로 다중 홉 토폴로지:

![다중 홉 전송](./media/vpn-gateway-bgp-overview/full-mesh-transit.png)

## <a name="bgp-faq"></a>BGP FAQ
[!INCLUDE [vpn-gateway-bgp-faq-include](../../includes/vpn-gateway-bpg-faq-include.md)]

## <a name="next-steps"></a>다음 단계
참조 [Azure VPN 게이트웨이에서 BGP 시작](vpn-gateway-bgp-resource-manager-ps.md) 크로스-프레미스 및 VNet 대 VNet 연결에 대 한 단계 tooconfigure BGP에 대 한 합니다.

