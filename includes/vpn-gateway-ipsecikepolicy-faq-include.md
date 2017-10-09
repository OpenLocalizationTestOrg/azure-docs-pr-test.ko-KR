### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>사용자 지정 IPsec/IKE 정책은 모든 Azure VPN Gateway SKU에서 지원되나요?
사용자 지정 IPsec/IKE 정책은 **VpnGw1, VpnGw2, VpnGw3, 표준** 및 **HighPerformance** VPN Gateway에서 지원됩니다. **기본** SKU는 지원되지 않습니다.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>연결에서 얼마나 많은 정책을 지정할 수 있나요?
지정된 연결에 대해 ***하나의*** 정책 조합만 지정할 수 있습니다.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>연결에 대해 부분적 정책을 지정할 수 있나요? (예: IPsec을 제외하고 IKE 알고리즘만)
아니요, IKE(주 모드) 및 IPsec(빠른 모드) 모두에 대한 모든 알고리즘 및 매개 변수를 지정해야 합니다. 부분 정책 지정은 허용되지 않습니다.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Hello 알고리즘 및 키 길이 hello 사용자 지정 정책에서 지원 되는 것이 무엇입니까?
hello 아래 표에 지원 hello 암호화 알고리즘 및 키 길이 hello 고객이 구성 가능 합니다. 모든 필드에 대해 한 가지 옵션을 선택해야 합니다.

| **IPsec/IKEv2**  | **옵션**                                                                   |
| ---              | ---                                                                           |
| IKEv2 암호화 | AES256, AES192, AES128, DES3, DES                                             |
| IKEv2 무결성  | SHA384, SHA256, SHA1, MD5                                                     |
| DH 그룹         | DHGroup24, ECP384, ECP256, DHGroup14(DHGroup2048), DHGroup2, DHGroup1, 없음 |
| IPsec 암호화 | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, 없음      |
| IPsec 무결성  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| PFS 그룹        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, 없음                              |
| QM SA 수명   | 초(정수, **최소 300**/기본값 27,000초)<br>KB(정수, **최소 1,024**/기본값 102,400,000KB)           |
| 트래픽 선택기 | UsePolicyBasedTrafficSelectors($True/$False, 기본값: $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048는 hello 동일 Diffie-hellman 그룹으로 **14** IKE 및 IPsec PFS 합니다. 참조 하십시오 [Diffie-hellman 그룹](#DH) hello에 대 한 매핑을 완료 합니다.
> 2. 지정 해야 GCMAES 알고리즘에 대 한 IPsec 암호화와 무결성에 대 한 동일한 GCMAES 알고리즘 및 키 길이 hello 합니다.
> 3. Hello Azure VPN 게이트웨이 28, 800 초 IKEv2 주 모드 SA 수명 동안 고정 됩니다.
> 4. QM SA 수명은 선택적 매개 변수입니다. 지정되지 않으면 기본값인 27,000초(7.5시간) 및 102,400,000KB(102GB)가 사용됩니다.
> 5. UsePolicyBasedTrafficSelector는 hello 연결에는 옵션 매개 변수입니다. Hello 다음 FAQ를 참조 하십시오 "UsePolicyBasedTrafficSelectors"에 대 한 항목

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>모든 Azure VPN 게이트웨이 정책 hello와 내 온-프레미스 VPN 장치 구성 간의 toomatch에 필요 합니까?
온-프레미스 VPN 장치 구성 접두사와 일치 하거나 hello 다음 알고리즘을 포함 하 고 매개 변수에서 지정 하는 hello Azure IPsec/IKE 정책:

* IKE 암호화 알고리즘
* IKE 무결성 알고리즘
* DH 그룹
* IPsec 암호화 알고리즘
* IPsec 무결성 알고리즘
* PFS 그룹
* 트래픽 선택기(*)

SA hello 수명 사양임 로컬, toomatch 필요는 없습니다.

사용 하도록 설정 하면 **UsePolicyBasedTrafficSelectors**, VPN 장치에는 모든 조합의 hello에서 온-프레미스 네트워크 (로컬 네트워크 게이트웨이) 접두사를 사용 하 여 정의 하는 트래픽을 선택기와 일치 하는 hello tooensure 필요 Azure 가상 네트워크 접두사 any-에-any 대신 사용 합니다. 예를 들어 온-프레미스 네트워크 접두사는 10.1.0.0/16 및 10.2.0.0/16, 하는 경우 가상 네트워크 접두사는 192.168.0.0/16 및 172.16.0.0/16 트래픽 선택기 뒤 toospecify hello가 필요 합니다.
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

너무 참조[여러 온-프레미스 정책 기반 VPN 장치 연결](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) 방법에 대 한 자세한 내용은 toouse이이 옵션입니다.

### <a name ="DH"></a>어떤 Diffie-Hellman 그룹이 지원됩니까?
hello 아래 표에 지원 되는 hello Diffie-hellman 그룹 IKE (DHGroup) 및 IPsec (PFSGroup):

| **Diffie-Hellman 그룹**  | **DHGroup**              | **PFSGroup** | **키 길이** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | 768비트 MODP   |
| 2                         | DHGroup2                 | PFS2         | 1024비트 MODP  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | 2048비트 MODP  |
| 19                        | ECP256                   | ECP256       | 256비트 ECP    |
| 20                        | ECP384                   | ECP284       | 384비트 ECP    |
| 24                        | DHGroup24                | PFS24        | 2048비트 MODP  |
|                           |                          |              |                |

너무 참조[RFC3526](https://tools.ietf.org/html/rfc3526) 및 [RFC5114](https://tools.ietf.org/html/rfc5114) 내용을 확인 합니다.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>사용자 지정 정책 hello hello Azure VPN 게이트웨이에 대 한 기본 IPsec/IKE 정책 집합을 대체 됩니까?
예, 사용자 지정 정책이 연결에서 지정 된 후 Azure VPN 게이트웨이 IKE 개시자와 응답 자가 IKE로 모두 hello 연결에서 hello 정책은만 사용 됩니다.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>IPsec/IKE 정책을 사용자 지정을 제거 하는 경우는 hello 연결 되 면 보호 되지 않는?
아니요, hello 연결 여전히 IPsec/IKE에 의해 보호 됩니다. Hello Azure VPN 게이트웨이 백 toohello 되돌아갑니다 연결에서 사용자 지정 정책 hello를 제거 하면 [기본 IPsec/IKE 제안 목록을](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) 및 hello 온-프레미스 VPN 장치를 사용 하 여 다시 IKE 핸드셰이크를 다시 시작 합니다.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>IPsec/IKE 정책을 추가 또는 업데이트하는 것이 VPN 연결에 방해가 될까요?
Hello Azure VPN 게이트웨이에서는 hello 기존 연결을 종료 되었다가 다시 시작 하는 IKE 핸드셰이크 toore hello (몇 초)는 작은 중단 될 수 예,-hello 새 암호화 알고리즘 및 매개 변수와 함께 hello IPsec 터널을 설정 합니다. 온-프레미스 VPN 장치는 hello 일치 하는 알고리즘 및 키 길이 toominimize hello 중단 구성도 확인 하십시오.

### <a name="can-i-use-different-policies-on-different-connections"></a>다른 연결에 다른 정책을 사용할 수 있나요?
예. 사용자 지정 정책은 각 연결 단위로 적용됩니다. 다른 연결에 서로 다른 IPsec/IKE 정책을 만들어 적용할 수 있습니다. 또한 tooapply 연결의 하위 집합에 사용자 지정 정책을 선택할 수 있습니다. 나머지 hello hello Azure 기본 IPsec/IKE 정책 집합을 사용 합니다.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>Hello 사용자 지정 정책에서 VNet 대 VNet 연결도 사용할 수 있습니까?
예, IPsec 프레미스 간 연결 또는 VNet 간 연결 모두에 사용자 지정 정책을 적용할 수 있습니다.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>Toospecify 필요 한가요 VNet 대 VNet 연결 리소스 모두에 동일한 정책을 hello?
예. Azure에서 VNet 간 터널은 두 개의 연결 리소스(각 방향당 하나씩)로 구성됩니다. 두 연결 리소스 tooensure 해야 hello 동일한 정책을 othereise hello VNet 대 VNet 연결을 설정 하지 것입니다.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>ExpressRoute 연결에서 사용자 지정 IPsec/IKE 정책이 작동하나요?
아니요. 정책 IPsec/IKE S2S VPN 및 hello Azure VPN 게이트웨이 통한 VNet 대 VNet 연결에 대해서만 작동 합니다.
