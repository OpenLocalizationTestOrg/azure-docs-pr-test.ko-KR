hello PolicyBased 및 RouteBased VPN 게이트웨이에 대 한 테이블 목록을 hello 요구 사항을 준수 합니다. 이 테이블 tooboth hello 리소스 관리자 및 클래식 배포 모델을 적용합니다. Hello 클래식 모델에 대 한이 PolicyBased VPN 게이트웨이 동일한 정적 게이트웨이로 hello 및 경로 기반 게이트웨이 동일 동적 게이트웨이로 hello 됩니다.

|  | **PolicyBased 기본 VPN 게이트웨이** | **RouteBased 기본 VPN 게이트웨이** | **RouteBased 표준 VPN 게이트웨이** | **RouteBased 고성능 VPN 게이트웨이** |
| --- | --- | --- | --- | --- |
| **사이트 간 연결(S2S)** |PolicyBased VPN 구성 |RouteBased VPN 구성 |RouteBased VPN 구성 |RouteBased VPN 구성 |
| **지점 및 사이트 간 연결(P2S)** |지원되지 않음 |지원됨(S2S와 함께 사용할 수 있음) |지원됨(S2S와 함께 사용할 수 있음) |지원됨(S2S와 함께 사용할 수 있음) |
| **인증 방법** |미리 공유한 키 |-S2S 연결에 대해 미리 공유한 키 -P2S 연결용 인증서 |-S2S 연결에 대해 미리 공유한 키 -P2S 연결용 인증서 |-S2S 연결에 대해 미리 공유한 키 -P2S 연결용 인증서 |
| **S2S 연결의 최대 수** |1 |10 |10 |30 |
| **P2S 연결의 최대 수** |지원되지 않음 |128 |128 |128 |
| **활성 라우팅 지원(BGP)** |지원되지 않음 |지원되지 않음 |지원됨 |지원됨 |

