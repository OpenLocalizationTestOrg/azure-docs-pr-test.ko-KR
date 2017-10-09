가상 네트워크 게이트웨이 만들 때 toospecify hello 게이트웨이 SKU toouse 되도록 해야 합니다. 작업 부하, 처리량, 기능 및 Sla의 hello 유형을 기반으로 하는 요구 사항을 충족 하는 hello Sku를 선택 합니다.

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <a name="workloads"></a>프로덕션 *vs.* 개발=테스트 워크로드

프로덕션에 대 한 Sku 다음 hello Sla 및 기능 집합, toohello 차이 때문 권장 *비교* 개발 테스트:

| **워크로드**                       | **SKU**               |
| ---                                | ---                    |
| **프로덕션, 중요한 워크로드** | VpnGw1, VpnGw2, VpnGw3 |
| **개발-테스트 또는 개념 증명**   | Basic                  |
|                                    |                        |

이전 hello를 사용 하는 표준 및 HighPerformance Sku Sku, hello 프로덕션 SKU 권장 됩니다. Hello에 대 한 내용은 이전 Sku 참조 [게이트웨이 Sku (레거시 Sku)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md)합니다.

###  <a name="feature"></a>게이트웨이 SKU 기능 집합

hello 새로운 게이트웨이 Sku 약식 hello 기능 집합이 제공 hello 게이트웨이:

| **SKU**| **기능**|
| ---    | ---         |
|**Basic**   | **경로 기반 VPN**: P2S를 사용하는 10개의 터널<br><br>**정책 기반 VPN**: (IKEv1): 1개의 터널. P2S 없음|
| **VpnGw1, VpnGw2 및 VpnGw3** | **경로 기반 VPN**: P2S, BGP, too30 터널 (*)을 활성-활성, 사용자 지정 IPsec/IKE 정책, ExpressRoute/v p N 공존 |
|        |             |

(*) "PolicyBasedTrafficSelectors" tooconnect는 경로 기반 VPN 게이트웨이 (VpnGw1, VpnGw2, VpnGw3) toomultiple 온-프레미스 방화벽 정책 기반 장치를 구성할 수 있습니다. 너무 참조[연결 VPN 게이트웨이 toomultiple 온-프레미스 PowerShell을 사용 하 여 정책 기반 VPN 장치](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) 대 한 자세한 내용은 합니다.

###  <a name="resize"></a>게이트웨이 SKU 크기 조정

1. VpnGw1, VpnGw2와 VpnGw3 SKU 간에 크기를 조정할 수 있습니다.
2. Hello 오래 된 게이트웨이 Sku 사용할 때는 Basic, Standard 및 HighPerformance Sku 간에 크기를 조정할 수 있습니다.
2. 하면 **없습니다** HighPerformance/Standard/Basic Sku toohello에서 크기 조정 새 VpnGw1/VpnGw2/VpnGw3 Sku입니다. 대신, 해야 [마이그레이션할](#migrate) toohello 새 Sku입니다.

###  <a name="migrate"></a>이전 Sku toohello에서 마이그레이션 새 Sku

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
