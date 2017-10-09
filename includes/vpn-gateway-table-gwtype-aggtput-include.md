Azure는 VPN 게이트웨이 Sku 다음 hello를 제공 합니다.

|**SKU**   | **S2S/VNet 간<br>터널** | **P2S<br>연결** | **집계<br>처리량 벤치마크** |
|---       | ---                             | ---                    | ---                         |
|**VpnGw1**| 최대 30                         | 최대 128               | 650Mbps                    |
|**VpnGw2**| 최대 30                         | 최대 128               | 1Gbps                      |
|**VpnGw3**| 최대 30                         | 최대 128               | 1.25Gbps                   |
|**Basic** | 최대 10                         | 최대 128               | 100Mbps                    | 
|          |                                 |                        |                             | 

- 집계 처리량 벤치마크는 단일 게이트웨이를 통해 집계된 여러 터널의 측정값을 기반으로 합니다. 기한 tooInternet 트래픽 조건 및 응용 프로그램 동작 보장 된 처리량 아닙니다.

- Hello에서 가격 책정 정보를 확인할 수 있습니다 [가격 책정](https://azure.microsoft.com/pricing/details/vpn-gateway) 페이지.

- Hello에 SLA (서비스 수준 계약) 정보를 찾을 수 [SLA](https://azure.microsoft.com/support/legal/sla/vpn-gateway/) 페이지.
