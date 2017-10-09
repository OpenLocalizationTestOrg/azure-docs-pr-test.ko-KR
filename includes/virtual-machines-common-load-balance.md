

Azure 인프라 서비스에 사용할 수 있는 두 가지 수준의 부하 분산이 있습니다.

* **DNS 수준**: 트래픽 toodifferent 클라우드 서비스에 대 한 부하 분산에 서로 다른 데이터 센터, 다른 데이터 센터 또는 tooexternal에 있는 toodifferent Azure 웹 사이트 끝점입니다. Azure 트래픽 관리자를 사용 하 여 이렇게 및 hello 라운드 로빈 부하 분산 방법입니다.
* **네트워크 수준**: 부하 분산의 클라우드 서비스의 들어오는 인터넷 트래픽 toodifferent 가상 컴퓨터 또는 클라우드 서비스 또는 가상 네트워크에 가상 컴퓨터 간의 트래픽을 분산을 로드 합니다. 이 hello Azure 부하 분산 장치와 함께 수행 됩니다.

## <a name="traffic-manager-load-balancing-for-cloud-services-and-websites"></a>클라우드 서비스 및 웹 사이트를 위한 트래픽 관리자 부하 분산
트래픽 관리자의 클라우드 서비스, 웹 사이트, 외부 사이트 및 다른 트래픽 관리자 프로필을 포함할 수 있는 사용자 트래픽 tooendpoints toocontrol hello 배포를 사용 합니다. 트래픽 관리자는 인터넷 리소스의 hello 도메인 이름에 대 한는 지능적인 정책 엔진 tooDomain (DNS 이름) 쿼리를 적용 하 여 작동 합니다. 클라우드 서비스나 웹 사이트 hello 세계 다른 데이터 센터에서 실행 될 수 있습니다.

Windows PowerShell 또는 REST tooconfigure 외부 끝점 또는 트래픽 관리자 프로필 끝점으로 사용 해야 합니다.

트래픽 관리자는 3 메서드 toodistribute 트래픽 부하 분산:

* **장애 조치**: 모든 트래픽을 toouse 기본 끝점을 싶지만 기본 hello를 사용할 수 없게 될 경우 백업을 제공 하는 경우이 방법을 사용 합니다.
* **성능**: 서로 다른 지리적 위치에 끝점 있고 요청 하는 "클라이언트 toouse hello 가까운" 끝점 hello 가장 짧은 대기 시간을 원하는 경우이 방법을 사용 합니다.
* **라운드 로빈:** hello에서 toodistribute 부하의 클라우드 서비스 같은 하려는 경우이 메서드를 사용 하 여 데이터 센터 또는 클라우드 서비스 또는 다른 데이터 센터의 웹 사이트 간에 합니다.

자세한 내용은 [트래픽 관리자 부하 분산 방법](../articles/traffic-manager/traffic-manager-routing-methods.md)(영문)을 참조하세요.

다음 다이어그램 hello hello 서로 다른 클라우드 서비스 간에 트래픽을 분산 시키고에 대 한 라운드 로빈 부하 분산 방법의 예를 보여 줍니다.

![loadbalancing](./media/virtual-machines-common-load-balance/TMSummary.png)

hello 기본 프로세스는 hello 다음.

1. 인터넷 클라이언트는 도메인 이름을 해당 tooa 웹 서비스를 쿼리합니다.
2. DNS 이름 쿼리 요청 tooTraffic hello 관리자를 전달합니다.
3. 트래픽 관리자 라운드 로빈 목록 hello에 hello 다음 클라우드 서비스를 선택 하 고 다시 전송 hello DNS 이름입니다. hello 인터넷 클라이언트의 DNS 서버 hello 이름 tooan IP 주소를 확인 하 고 인터넷 클라이언트 toohello 보냅니다.
4. hello 인터넷 클라이언트에서 트래픽 관리자를 선택 하는 hello 클라우드 서비스와 연결 합니다.

자세한 내용은 [트래픽 관리자](../articles/traffic-manager/traffic-manager-overview.md)(영문)를 참조하십시오.

## <a name="azure-load-balancing-for-virtual-machines"></a>가상 컴퓨터를 위한 Azure 부하 분산
가상 컴퓨터에 hello 동일한 클라우드 서비스 또는 가상 네트워크와 직접 자신의 개인 IP 주소를 사용 하 여 서로 통신할 수 있습니다. 클라우드 서비스 컴퓨터와 hello 외부 서비스 또는 클라우드 서비스 또는 구성 된 끝점을 사용 하 여 가상 네트워크에 가상 컴퓨터와 가상 네트워크의 통신만 가능 합니다. 끝점의 공용 IP 주소와 포트 toothat 개인 IP 주소 매핑 및 포트는 가상 컴퓨터 또는 Azure 클라우드 서비스 내에서 웹 역할은.

hello Azure 부하 분산 장치는 여러 가상 컴퓨터 또는 부하 분산 된 집합 이라는 구성에서 서비스는 특정 유형의 들어오는 트래픽 임의로 분산 합니다. 예를 들어 여러 웹 서버 또는 웹 역할에서 웹 요청 트래픽의 hello 부하를 분배할 수 있습니다.

hello 다음 그림에 hello 공용 및 개인 TCP 포트 80에 대 한 세 개의 가상 컴퓨터 간에 공유 되는 표준 (암호화 되지 않은) 웹 트래픽에 대 한 부하 분산 된 끝점입니다. 이 세 대의 가상 컴퓨터는 부하 분산 집합에 속합니다.

![loadbalancing](./media/virtual-machines-common-load-balance/LoadBalancing.png)

자세한 내용은 [Azure 부하 분산 장치](../articles/load-balancer/load-balancer-overview.md)(영문)를 참조하세요. Hello 부하 분산 집합 toocreate를 단계에 대 한 참조 [부하 분산 된 집합 구성](../articles/load-balancer/load-balancer-get-started-internet-arm-ps.md)합니다.

Azure는 클라우드 서비스 또는 가상 네트워크 내에서 부하를 분산할 수도 있습니다. 이 내부 부하 분산 이라고와 hello 같은 방법으로 다음에 사용할 수 있습니다.

* (예를 들어 웹 계층과 데이터베이스 계층) 간 다중 계층 응용 프로그램의 다양 한 계층의 서버 간 tooload 밸런스 합니다.
* (tooload 균형 기간 업무 LOB) 응용 프로그램 추가 부하 분산 장치 하드웨어 또는 소프트웨어 없이 Azure에서 호스트 합니다.
* tooinclude 온-프레미스 서버 hello 집합이 컴퓨터 트래픽의 부하가 분산 됩니다.

내부 부하 분산 된 집합을 구성 하 여 비슷한 tooAzure 부하 분산, 내부 부하 분산은 지원 됩니다.

다음 다이어그램 hello 크로스-프레미스 가상 네트워크에 3 개의 가상 컴퓨터 간에 공유 되는 기간 업무 (LOB) 응용 프로그램에 대 한 내부 부하 분산 된 끝점의 예를 보여 줍니다.

![loadbalancing](./media/virtual-machines-common-load-balance/LOBServers.png)

## <a name="load-balancer-considerations"></a>부하 분산 장치 고려 사항
부하 분산 장치는 기본적으로 구성 된 4 분의 유휴 세션 tootimeout 합니다. 응용 프로그램 부하 분산 장치 뒤 연결 유휴 4 분에 대 한 고 Keep-alive 구성 되어 있지 않습니다, hello 연결이 삭제 됩니다. 부하 분산 장치 동작 tooallow hello를 변경할 수는 [Azure 부하 분산 장치에 대 한 긴 시간 제한 설정을](../articles/load-balancer/load-balancer-tcp-idle-timeout.md)합니다.

다른 고려 사항은 hello 유형의 Azure 부하 분산 장치에서 지 원하는 배포 모드입니다. 원본 IP 선호도(원본 IP, 대상 IP) 또는 원본 IP 프로토콜(원본 IP, 대상 IP 및 프로토콜)을 구성할 수 있습니다. 자세한 내용은 [Azure 부하 분산 장치 배포 모드(원본 IP 선호도)](../articles/load-balancer/load-balancer-distribution-mode.md) 를 확인하세요.

## <a name="next-steps"></a>다음 단계
Hello 부하 분산 집합 toocreate를 단계에 대 한 참조 [내부 부하 분산 된 집합 구성](../articles/load-balancer/load-balancer-get-started-ilb-arm-ps.md)합니다.

자세한 내용은 [내부 부하 분산](../articles/load-balancer/load-balancer-internal-overview.md)을 참조하세요.

