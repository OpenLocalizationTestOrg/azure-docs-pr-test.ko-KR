VNet 대 VNet FAQ hello tooVPN 게이트웨이 연결을 적용합니다. VNet 피어링을 찾으려면 [가상 네트워크 피어링](../articles/virtual-network/virtual-network-peering-overview.md)을 참조하세요.

### <a name="does-azure-charge-for-traffic-between-vnets"></a>Azure는 VNet 간 트래픽에 요금을 청구하나요?

Hello 내에서 VNet 대 VNet 트래픽이 동일 지역은 VPN 게이트웨이 연결을 사용 하는 경우 양방향에 대 한 무료입니다. 지역 VNet 대 VNet 송신 간 트래픽 hello 소스 지역을 기반으로 하는 hello 간 VNet 아웃 바운드 데이터 전송 속도 대금이 청구 됩니다. Toohello 참조 [VPN 게이트웨이 가격 책정 페이지](https://azure.microsoft.com/pricing/details/vpn-gateway/) 대 한 자세한 내용은 합니다. VNet 피어 링을 보다는 VPN 게이트웨이 사용 하 여 Vnet을 연결 하는 경우 참조 hello [가격 책정 페이지 가상 네트워크](https://azure.microsoft.com/pricing/details/virtual-network/)합니다.

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>VNet 대 VNet 트래픽이 hello 인터넷 거쳐야가?

아니요. VNet 대 VNet 트래픽이 hello backbone Microsoft Azure hello 인터넷 하지을 통과 합니다.

### <a name="is-vnet-to-vnet-traffic-secure"></a>VNet 간 트래픽은 안전한가요?

예, IPsec/IKE 암호화로 보호됩니다.

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>VPN 장치 tooconnect Vnet을 함께 필요 수행 합니까?

아니요. 크로스-프레미스 연결이 필요한 경우가 아니면 여러 Azure 가상 네트워크를 함께 연결할 때 VPN 장치는 필요하지 않습니다.

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>Vnet 내 hello에 toobe 필요가 동일한 지역?

아니요. hello에 hello 가상 네트워크 수 같거나 다른 Azure 지역 (위치).

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>Hello Vnet에는 없는 경우 hello 동일한 구독을 hello 구독 필요가 hello 동일한 AD 테 넌 트와 연결 된 toobe?

아니요.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>VNet간 연결을 멀티 사이트 연결과 함께 사용할 수 있나요?

예. 가상 네트워크 연결을 다중 사이트 VPN과 동시에 사용할 수 있습니다.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>하나의 가상 네트워크에 연결할 수 있는 온-프레미스 사이트 및 가상 네트워크 수는 어떻게 됩니까?

[게이트웨이 요구 사항](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) 테이블을 참조하세요.

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>VNet 대 VNet tooconnect Vm을 사용 하거나 클라우드 서비스는 VNet 외부에서 수 있습니까?

아니요. VNet 간 연결은 가상 네트워크 연결을 지원합니다. 가상 네트워크에 포함되어 있지 않은 가상 컴퓨터 또는 클라우드 서비스 연결은 지원되지 않습니다.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>클라우드 서비스 또는 부하 분산 끝점이 VNet까지 이어지나요?

아니요. 클라우드 서비스 또는 부하 분산 끝점은 연결되어 있더라도 여러 가상 네트워크에 분산될 수 없습니다.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>VNet 간 또는 멀티 사이트 연결에 PolicyBased VPN 유형을 사용할 수 있나요?

아니요. VNet 간 연결 및 멀티 사이트 연결에는 RouteBased(이전 명칭: 동적 라우팅) VPN 유형의 Azure VPN 게이트웨이가 필요합니다.

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>연결할 수 있습니까 VNet RouteBased VPN 유형을 tooanother VNet으로 PolicyBased VPN 형식과?

아니요, 두 가상 네트워크는 모두 경로 기반(이전 명칭: 동적 라우팅) VPN을 사용해야 합니다.

### <a name="do-vpn-tunnels-share-bandwidth"></a>VPN 터널은 대역폭을 공유하나요?

예. Hello 가상 네트워크의 모든 VPN 터널 hello hello Azure VPN 게이트웨이 사용 가능한 대역폭을 공유 하 고 Azure에서 동일한 VPN 게이트웨이 작동 시간 SLA hello 합니다.

### <a name="are-redundant-tunnels-supported"></a>중복 터널이 지원되나요?

하나의 가상 네트워크 게이트웨이를 active-active로 구성하면 한 쌍의 가상 네트워크 사이의 중복 터널이 지원됩니다.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>VNet 간 구성에 대해 겹치는 주소 공간을 가질 수 있나요?

아니요. 겹치는 IP 주소 범위를 가질 수 있습니다.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>연결된 가상 네트워크와 온-프레미스 로컬 사이트 사이에 겹치는 주소 공간이 있을 수 있나요?

아니요. 겹치는 IP 주소 범위를 가질 수 있습니다.



