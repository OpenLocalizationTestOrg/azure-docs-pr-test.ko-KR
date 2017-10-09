hello 레거시 (이전) VPN 게이트웨이 Sku는:

* Basic
* Standard
* HighPerformance

VPN 게이트웨이 hello UltraPerformance 게이트웨이 SKU를 사용 하지 않습니다. Hello UltraPerformance SKU에 대 한 정보를 참조 hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) 설명서입니다.

작업할 때 레거시 Sku hello hello 다음을 고려 하십시오.

* PolicyBased VPN 유형을 toouse 하려는 경우 Basic SKU hello를 사용 해야 합니다. 정책 기반 VPN(이전에는 정적 라우팅이라고 함)은 다른 SKU에서 지원되지 않습니다.
* BGP은 hello Basic SKU에서 지원 되지 않습니다.
* ExpressRoute VPN 게이트웨이 함께 사용할 구성은 hello Basic SKU에서 지원 되지 않습니다.
* Hello HighPerformance SKU에 대 한 액티브-액티브 S2S VPN 게이트웨이 연결을 구성할 수 있습니다.
