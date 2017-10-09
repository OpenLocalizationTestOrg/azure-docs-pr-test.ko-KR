### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>지점 및 사이트 간 연결에 사용할 수 있는 클라이언트 운영 체제는 무엇입니까?

다음 클라이언트 운영 체제 hello 지원 됩니다.

* Windows 7(32비트 및 64비트)
* Windows Server 2008 R2(64비트 전용)
* Windows 8(32비트 및 64비트)
* Windows 8.1(32비트 및 64비트)
* Windows Server 2012(64비트 전용)
* Windows Server 2012 R2(64비트 전용)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>SSTP를 지원하는 지점 및 사이트 간 연결에 소프트웨어 VPN 클라이언트를 사용할 수 있습니까?

아니요. 지원 제한만 toohello Windows 운영 체제 버전 위에 나열 됩니다.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>지점 및 사이트 간 구성에서 VPN 클라이언트 끝점을 몇 개까지 지정할 수 있습니까?

지원 too128 VPN 클라이언트 toobe 수 tooconnect tooa 가상 네트워크를 hello에서 동일한 시간입니다.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>지점 및 사이트 간 연결에 내부 PKI 루트 CA를 사용할 수 있습니까?

예. 이전에는 자체 서명한 루트 인증서만 사용할 수 있었습니다. 여전히 20개의 루트 인증서를 업로드할 수 있습니다.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>지점 및 사이트 간 기능을 사용하여 프록시와 방화벽을 트래버스할 수 있습니까?

예. 방화벽을 통해 tootunnel SSTP (Secure Socket Tunneling Protocol)를 사용합니다. 이 터널은 HTTP 연결로 표시됩니다.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>지점 및 사이트에 대해 구성 된 클라이언트 컴퓨터를 다시 시작 하는 경우 hello VPN 자동으로 다시 연결 됩니다.

기본적으로 hello 클라이언트 컴퓨터는 다시 설정 하지 않도록 hello VPN 연결이 자동으로 합니다.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>자동 다시 연결 지점 및 사이트 지원의 역할과에서 DDNS VPN 클라이언트 hello?

자동 다시 연결과 DDNS는 현재 지점 및 사이트 간 VPN에서 지원되지 않습니다.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>사용할 수 있습니까 사이트 간 및 지점 및 사이트 간 구성이 공존할 수 hello에 대 한 동일한 가상 네트워크?

예. 게이트웨이에 경로 기반 VPN 유형이 있는 경우 이 솔루션이 모두 작동합니다. Hello 클래식 배포 모델에 대 한 동적 게이트웨이가 필요 합니다. 수행할 하지 지원 지점 및 사이트 간 게이트웨이 hello를 사용 하 여 또는 정적 라우팅 VPN 게이트웨이 대 한 `-VpnType PolicyBased` cmdlet.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>Hello에는 지점 및 사이트 클라이언트 tooconnect toomultiple 가상 네트워크를 구성할 수 동시?

예, 구성할 수 있습니다. 하지만 hello 가상 네트워크는 겹치는 IP 접두사를 사용할 수 없습니다 및 hello 지점 및 사이트 간 주소 공간 hello 가상 네트워크 간에 겹치지 않아야 합니다.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>사이트 간 연결 또는 지점 및 사이트 간 연결을 통해 어느 정도의 처리량을 제공할 수 있습니까?

것은 어려운 toomaintain hello VPN 터널의 hello 정확한 처리량입니다. IPsec과 SSTP는 암호화 중심 VPN 프로토콜입니다. 또한 프레미스 및 hello 인터넷 간 대역폭과 hello 대기 시간에 처리량이 제한 됩니다.
