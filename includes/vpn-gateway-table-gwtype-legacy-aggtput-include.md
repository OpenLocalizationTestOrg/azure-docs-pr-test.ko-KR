hello 다음 표에 hello 게이트웨이 유형 및 집계 처리량을 예상된 hello SKU 게이트웨이에서 있습니다. 이 테이블 toohello 리소스 관리자 및 클래식 배포 모델을 적용합니다. 

가격 책정은 게이트웨이 SKU마다 다릅니다. 자세한 내용은 [VPN Gateway 가격 책정](https://azure.microsoft.com/pricing/details/vpn-gateway)을 참조하세요.

Note 해당 hello UltraPerformance 게이트웨이 SKU이이 테이블에 표시 되지 않습니다. Hello UltraPerformance SKU에 대 한 정보를 참조 hello [ExpressRoute](../articles/expressroute/expressroute-about-virtual-network-gateways.md) 설명서입니다.

|  | **VPN 게이트웨이 처리량(1)** | **VPN 게이트웨이 최대 IPsec 터널(2)** | **Express 경로 게이트웨이 처리량** | **VPN 게이트웨이 및 Express 경로 공존** |
| --- | --- | --- | --- | --- |
| **기본 SKU(3)(5)(6)** |100Mbps |10 |500Mbps(6) |아니요 |
| **표준 SKU(4)(5)** |100Mbps |10 |1000Mbps |예 |
| **고성능 SKU(4)** |200Mbps |30 |2000Mbps |예 |


(1) hello VPN 처리량 hello의 Vnet 간의 hello 측정값을 기반으로 대략적인 예상 값은 동일한 Azure 지역에 있습니다. 크로스-프레미스 연결에 대 한 보장된 처리량 hello 인터넷에서 것 hello 가능한 최대 처리량 측정 합니다.

(터널의 수 2) hello tooRouteBased Vpn을 참조 하십시오. 정책 기반 VPN는 하나의 사이트 간 VPN 터널을 지원할 수 있습니다.

(3) BGP hello Basic SKU에 대 한 지원 되지 않습니다.

(4) 정책 기반 VPN은 이 SKU에 지원되지 않습니다. 이러한 hello Basic SKU만 지원 됩니다.

(5) 이 SKU에 대한 활성-활성 S2S VPN Gateway 연결은 지원되지 않습니다. 액티브-액티브 hello HighPerformance SKU에서 지원 됩니다.

(6) 기본 SKU는 ExpressRoute와 함께 사용되지 않습니다.
