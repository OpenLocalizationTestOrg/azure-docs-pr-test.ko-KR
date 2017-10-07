---
title: "Azure ExpressRoute 채택에 대 한 aaaPrerequisites | Microsoft Docs"
description: "이 페이지에서는 Azure express 경로 회로 주문할 수 전에 충족 하는 요구 사항 toobe 목록을 제공 합니다."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
ms.assetid: f872d25e-acfd-405d-9d1b-dcb9f323a2ff
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/30/2017
ms.author: cherylmc
ms.openlocfilehash: 524c86f6570dc6e6505fe55323b8508e8eeff791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="expressroute-prerequisites--checklist"></a>ExpressRoute 필수 구성 요소 및 검사 목록
ExpressRoute를 사용 하 여 서비스를 필요한 tooverify hello 다음 섹션에에서 나열 된 요구 사항을 준수 하는 hello tooconnect tooMicrosoft 클라우드 사항이 충족 되었는지 확인 합니다.

[!INCLUDE [expressroute-office365-include](../../includes/expressroute-office365-include.md)]

## <a name="azure-account"></a>Azure 계정
* 유효한 활성 Microsoft Azure 계정 이 계정은 hello ExpressRoute 회로를 필요한 tooset입니다. ExpressRoute 회로는 Azure 구독 내의 리소스입니다. Azure 구독 요구 사항은 연결이 Office 365 서비스 Dynamics 365 등의 제한 된 toonon Azure Microsoft 클라우드 서비스입니다.
* 활성 Office 365 구독(Office 365 서비스를 사용하는 경우). 자세한 내용은 참조 hello [Office 365 특정 요구 사항](#office-365-specific-requirements) 이 문서의 섹션.

## <a name="connectivity-provider"></a>연결 공급자

* 작업할 수는 [ExpressRoute 연결 파트너](expressroute-locations.md#partners) tooconnect toohello Microsoft 클라우드입니다. [세 가지 방법](expressroute-introduction.md)으로 온-프레미스 네트워크와 Microsoft 간에 연결을 설정할 수 있습니다.
* 통해 toohello Microsoft 클라우드 공급자에 ExpressRoute 연결 파트너 없으면 계속 연결할 수 있습니다는 [클라우드 교환 공급자](expressroute-locations.md#connectivity-through-exchange-providers)합니다.

## <a name="network-requirements"></a>네트워크 요구 사항
* **중복 연결**: 사용자와 공급자 간 물리적 연결에서 중복성 요구 사항은 없습니다. Microsoft에만 있는 경우에 Microsoft의 라우터 및 hello 피어 링 라우터 간에 설정 하는 중복 BGP 세션 toobe 필요 [하나의 실제 연결 tooa 클라우드 교환](expressroute-faqs.md#onep2plink)합니다.
* **라우팅**: toohello Microsoft 클라우드를 연결 하는 방법에 따라 또는 공급자 tooset 필요한 및 관리에 대 한 BGP 세션 hello [라우팅 도메인](expressroute-circuit-peerings.md)합니다. 일부 이더넷 연결 공급자 또는 클라우드 Exchange 공급자는 가치 추가 서비스로 BGP 관리를 제공할 수 있습니다.
* **NAT**: Microsoft만 Microsoft 피어링을 통해 공용 IP 주소를 허용합니다. 또는 공급자 필요 tootranslate hello 개인 IP 주소 toohello 공용 IP 주소 개인 IP 주소로 온-프레미스 네트워크를 사용 하는 경우 [NAT hello를 사용 하 여](expressroute-nat.md)합니다.
* **QoS**: 비즈니스용 Skype에는 차별화된 QoS 처리를 필요로 하는 다양한 서비스(예: 음성, 비디오, 텍스트)가 있습니다. 및 공급자 hello 따라야 [QoS 요구 사항](expressroute-qos.md)합니다.
* **네트워크 보안**: 고려 [네트워크 보안](../best-practices-network-security.md) toohello ExpressRoute 통해 Microsoft 클라우드를 연결할 때.

## <a name="office-365"></a>Office 365
ExpressRoute에 tooenable Office 365를 계획 하는 경우 다음 문서를 Office 365 요구 사항에 대 한 자세한 내용은 hello를 검토 합니다.

* [Office 365용 ExpressRoute 개요](https://support.office.com/en-us/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd)
* [Office 365용 ExpressRoute로 라우팅](https://support.office.com/en-us/article/Routing-with-ExpressRoute-for-Office-365-e1da26c6-2d39-4379-af6f-4da213218408)
* [Office 365 URL 및 IP 주소 범위](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2)
* [Office 365에 대한 네트워크 계획 및 성능 조정](https://support.office.com/en-us/article/Network-planning-and-performance-tuning-for-Office-365-e5f1228c-da3c-4654-bf16-d163daee8848)
* [네트워크 대역폭 계산기 및 도구](https://support.office.com/en-us/article/Network-and-migration-planning-for-Office-365-f5ee6c33-bcd7-4b0b-b0f8-dc1d9fb8d132)
* [온-프레미스 환경과 Office 365 통합](https://support.office.com/en-us/article/Office-365-integration-with-on-premises-environments-263faf8d-aa21-428b-aed3-2021837a4b65)
* [Office 365 고급 교육 비디오의 ExpressRoute](https://channel9.msdn.com/series/aer/)

## <a name="dynamics-365"></a>Dynamics 365
ExpressRoute tooenable Dynamics 365 하려는 경우 다음 Dynamics 365 대 한 자세한 내용은 문서 hello 검토

* [Dynamics 365 및 ExpressRoute 백서](http://download.microsoft.com/download/B/2/8/B2896B38-9832-417B-9836-9EF240C0A212/Microsoft%20Dynamics%20365%20and%20ExpressRoute.pdf)
* [Dynamics 365 URL](https://support.microsoft.com/kb/2655102) 및 [IP 주소 범위](https://support.microsoft.com/kb/2728473)

## <a name="next-steps"></a>다음 단계
* ExpressRoute에 대 한 자세한 내용은 참조 hello [express 경로 FAQ](expressroute-faqs.md)합니다.
* ExpressRoute 연결 공급자를 찾습니다. [Express 경로 파트너 및 피어링 위치](expressroute-locations.md)를 확인하세요.
* 참조에 대 한 toorequirements [라우팅](expressroute-routing.md), [NAT](expressroute-nat.md), 및 [QoS](expressroute-qos.md)합니다.
* ExpressRoute 연결을 구성합니다.
  * [ExpressRoute 회로 만들기](expressroute-howto-circuit-classic.md)
  * [라우팅 구성](expressroute-howto-routing-classic.md)
  * [VNet tooan ExpressRoute 회로 연결](expressroute-howto-linkvnet-classic.md)
