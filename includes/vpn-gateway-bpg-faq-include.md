### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>BGP가 모든 Azure VPN Gateway SKU를 지원하나요?
아니요. BGP는 **표준** 및 **HighPerformance** VPN 게이트웨이에서 지원됩니다. **기본** SKU는 지원되지 않습니다.

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>Azure 정책 기반 VPN 게이트웨이에 BGP를 사용할 수 있나요?
아니요. BGP는 경로 기반 VPN 게이트웨이에서만 지원됩니다.

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>개인 ASN(자치 시스템 번호)을 사용할 수 있나요?
예. 온-프레미스 네트워크와 Azure 가상 네트워크 모두에 자체 공용 ASN 또는 개인 ASN을 사용할 수 있습니다.

### <a name="are-there-asns-reserved-by-azure"></a>Azure에서 예약된 ASN이 있나요?
예, hello 다음 Asn은 Azure에 의해 예약 내부 및 외부 피어 링에 대 한:

* 공용 ASN: 8075, 8076, 12076
* 개인 ASN: 65515, 65517, 65518, 65519, 65520

TooAzure VPN 게이트웨이 연결할 때 온-프레미스 VPN 장치에 대 한 이러한 Asn을 지정할 수 없습니다.

### <a name="are-there-any-other-asns-that-i-cant-use"></a>사용할 수 없는 다른 ASN이 있나요?
예, 다음 Asn hello 있습니다 [IANA에서 예약한](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml) Azure VPN 게이트웨이를 구성할 수 없습니다.

23456, 64496-64511, 65535-65551 및 429496729

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>사용할 수 있습니까 hello 둘 다에 동일한 ASN 온-프레미스 VPN 네트워크와 Azure Vnet?
아니요. 온-프레미스 네트워크와 Azure VNet을 함께 BGP에 연결하려면 서로 다른 ASN을 할당해야 합니다. 크로스 프레미스 연결에 대한 BGP 활성화 여부에 관계없이 Azure VPN 게이트웨이에 할당되는 기본 ASN은 65515입니다. Hello VPN 게이트웨이 만들 때 다른 ASN을 할당 하 여이 기본값을 재정의 하거나 hello 게이트웨이 만든 후 hello ASN을 변경할 수 있습니다. Tooassign Azure 로컬 네트워크 게이트웨이 해당 온-프레미스 Asn toohello에 필요 합니다.

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>어떤 주소 접두사는 Azure VPN 게이트웨이 보급 toome?
Azure VPN 게이트웨이 tooyour 온-프레미스 BGP 장치 경로 따라 hello를 보급 합니다.

* VNet 주소 접두어
* 각 로컬 네트워크 게이트웨이 연결 된 toohello Azure VPN 게이트웨이에 대 한 주소 접두사
* 다른 BGP 피어 링 세션 연결 된 toohello Azure VPN 게이트웨이 확인 경로 **기본 제외 하 고 경로 또는 경로와 겹칠 VNet 접두사**합니다.

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>기본 경로 (0.0.0.0/0) tooAzure VPN 게이트웨이 보급할 수 있습니까?
예.

온-프레미스 사이트를 위한 모든 VNet 송신 트래픽에 강제로이 및 됩니다 hello VNet Vm에서 허용 하지 않으려면 hello 인터넷에 직접 해당 하는 RDP 또는 SSH hello 인터넷 toohello Vm에서에서의 공용 통신이 note 하십시오.

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>내 가상 네트워크 접두사도 hello 정확한 접두사 보급

아니요, 동일한 가상 네트워크 주소 접두사 중 하나로 prefixes 광고 hello 차단 되거나 hello Azure 플랫폼으로 필터링 됩니다. 그러나 Virtual Network 내에 포함된 접두사의 상위 집합에 해당하는 접두사를 보급할 수 있습니다. 

예를 들어 가상 네트워크 주소 공간 10.0.0.0/16 hello를 사용 하는 경우 10.0.0.0/8을 광고할 수 있습니다. 10.0.0.0/16 또는 10.0.0.0/24는 보급할 수 없습니다.

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>내 VNet-VNet 연결에 BPG를 사용할 수 있나요?
예. 크로스 프레미스 연결과 VNet-VNet 연결에 모두 BGP를 사용할 수 있습니다.

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>BGP를 비 BGP 연결과 혼합하여 내 Azure VPN 게이트웨이에 사용할 수 있나요?
예, 두 BGP를 혼합할 수 있습니다 및 비 BGP 연결을 동일한 Azure VPN 게이트웨이에 hello 합니다.

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>Azure VPN 게이트웨이가 BGP 전송 라우팅을 지원하나요?
예, BGP 전송 라우팅을 지원 Azure VPN 게이트웨이 hello 예외로 **하지** 보급 기본 tooother BGP 피어를 라우팅합니다. tooenable 전송에서 여러 Azure VPN 게이트웨이 라우팅에서 활성화 해야 BGP 모든 중간 VNet 대 VNet 연결 합니다.

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>Azure VPN 게이트웨이와 내 온-프레미스 네트워크 간에 터널이 여러 개 있을 수 있나요?
예, Azure VPN 게이트웨이와 내 온-프레미스 네트워크 간에 S2S VPN 터널을 여러 개 구축할 수 있습니다. Azure VPN 게이트웨이에 대 한 터널의 hello 총 수에 대해 계산 됩니다. 이러한 모든 터널 및 두 터널에서 BGP를 사용 하도록 설정 해야 note 하십시오.

예를 들어 두 개의 중복 터널 Azure VPN 게이트웨이 온-프레미스 네트워크 사이 있으면 것을 사용 하면 2 터널 hello (표준에 대 한 10)에서 30 HighPerformance에 대 한 Azure VPN 게이트웨이에 대 한 총 할당량을 초과 합니다.

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>두 Azure VNet과 BGP와 간에 여러 터널이 있을 수 있나요?
예, 하지만 hello 가상 네트워크 게이트웨이 중 하나 이상이 활성-활성 구성에 있어야 합니다.

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>ExpressRoute/S2S VPN 동시 존재 구성에서 S2S VPN에 BGP를 사용할 수 있나요?
예. 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>Azure VPN 게이트웨이는 BGP 피어 IP에 어떤 주소를 사용하나요?
hello Azure VPN 게이트웨이 hello hello 가상 네트워크에 대해 정의 된 GatewaySubnet 범위에서에서 단일 IP 주소를 할당 합니다. 기본적으로이 hello 두 번째 마지막 주소 hello 범위입니다. 예를 들어 프로그램 GatewaySubnet 10.12.255.0/27 이면에서 사이의 값 10.12.255.0 too10.12.255.31, hello hello Azure VPN 게이트웨이에서 BGP 피어 IP 주소 10.12.255.30 됩니다. Hello Azure VPN 게이트웨이 정보를 나열 하는 경우이 정보를 찾을 수 있습니다.

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>Hello BGP 피어 IP 주소 내 VPN 장치에 대 한 hello 요구 사항은 무엇입니까?
사용자의 온-프레미스 BGP 피어 주소 **해서는 안** hello VPN 장치의 공용 IP 주소와 동일한 hello 수 있습니다. BGP 피어 IP에 대 한 hello VPN 장치에서 다른 IP 주소를 사용 합니다. Toohello 루프백 인터페이스 hello 장치에 할당 한 주소 수 있습니다. Hello 해당 로컬 네트워크 게이트웨이 나타내는 hello 위치에이 주소를 지정 합니다.

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>어떻게 해야 지정 로컬 네트워크 게이트웨이 hello에 대 한 주소 접두사 내로 BGP를 사용 하면?
로컬 네트워크 게이트웨이 azure hello 온-프레미스 네트워크에 대 한 hello 초기 주소 접두사를 지정합니다. BGP를 사용 hello 호스트 접두사를 할당 해야 합니다 (/ 32 접두사) hello 주소 공간 해당 온-프레미스 네트워크에 대 한 BGP 피어 IP 주소입니다. BGP 피어 IP 10.52.255.254 이면 "10.52.255.254/32" hello localNetworkAddressSpace로 hello이 온-프레미스 네트워크를 나타내는 로컬 네트워크 게이트웨이 지정 해야 합니다. 이 Azure VPN hello tooensure 게이트웨이 hello S2S VPN 터널을 통해 hello BGP 세션을 설정 합니다.

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>어떤 toomy 온-프레미스 VPN 장치 hello BGP 피어 링 세션에 대 한 추가 해야 합니까?
Toohello IPsec S2S VPN 터널을 가리키는 VPN 장치에서의 hello Azure BGP 피어 IP 주소가 호스트 경로 추가 해야 합니다. 예를 들어 hello Azure VPN 피어 IP 인 "10.12.255.30" VPN 장치에서 "10.12.255.30" hello 일치 하는 IPsec 터널 인터페이스의 다음 홉 인터페이스에 대 한 호스트 경로 추가 해야 합니다.

