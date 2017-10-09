* **PolicyBased:** PolicyBased Vpn hello 클래식 배포 모델에서 정적 라우팅 게이트웨이 이전에 호출 되었습니다. 정책 기반 Vpn 암호화 하 고 직접 hello에 따라 패킷을 IPsec 터널을 통해 온-프레미스 네트워크 및 hello Azure VNet 간의 주소 접두사의 hello 조합으로 구성 된 IPsec 정책. hello 정책 (또는 트래픽 선택기)은 일반적으로 hello VPN 장치 구성에 대 한 액세스 목록으로 정의 됩니다. PolicyBased VPN 형식에 대 한 hello 값은 *PolicyBased*합니다. PolicyBased VPN을 사용할 경우 다음과 같은 제한을 고려 hello에 유의 하십시오.
  
  * PolicyBased Vpn 수 **만** hello 기본 게이트웨이 SKU에서 사용할 수 있습니다. 이 VPN 유형은 다른 게이트웨이 SKU와 호환되지 않습니다.
  * PolicyBased VPN을 사용하는 경우 터널 1개만 허용됩니다.
  * S2S 연결 및 특정 구성에 대해서만 PolicyBased VPN을 사용할 수 있습니다. 대부분의 VPN 게이트웨이 구성에는 RouteBased VPN이 필요합니다.
* **RouteBased**: RouteBased Vpn hello 클래식 배포 모델에서 동적 라우팅 게이트웨이 이전에 호출 되었습니다. RouteBased Vpn hello ip 전달 또는 해당 터널 인터페이스에 테이블 toodirect 패킷을 라우팅하려면 "라우팅"를 사용 합니다. hello 터널 인터페이스 다음 암호화 또는 hello 패킷에 hello 터널 내부 및 외부 암호를 해독 합니다. RouteBased Vpn으로 any-에-모든 구성에 대 한 정책 (또는 트래픽 선택기) hello (또는 와일드 카드). RouteBased VPN 형식에 대 한 hello 값은 *RouteBased*합니다.

