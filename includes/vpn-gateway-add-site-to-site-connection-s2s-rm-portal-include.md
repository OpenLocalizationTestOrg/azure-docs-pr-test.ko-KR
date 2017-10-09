1. 가상 네트워크 게이트웨이에 대 한 tooand 열려 hello 블레이드를 이동 합니다. 여러 방법으로 toonavigate 가지가 있습니다. Toohello 게이트웨이 'VNet1GW' 너무 이동 하 여 탐색 했습니다 예에서**TestVNet1 개요-> 연결 됨-> 장치 VNet1GW->**합니다.
2. VNet1GW에 대 한 hello 블레이드에서 클릭 **연결**합니다. Hello 연결 블레이드의 hello 위쪽 클릭 **+ 추가** tooopen hello **연결 추가** 블레이드입니다.

    ![사이트 간 연결 만들기](./media/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include/connection1.png)

3. Hello에 **연결 추가** 블레이드에서 hello에서 전체 값 toocreate 연결 합니다.

  - **이름:** 연결의 이름을 지정합니다. 예제에서 **VNet1toSite2**를 사용합니다.
  - **연결 형식:** **사이트 간(IPSec)**을 선택합니다.
  - **가상 네트워크 게이트웨이:** hello 값이이 게이트웨이의에서 연결 하는 때문에 고정 됩니다.
  - **로컬 네트워크 게이트웨이:** 클릭 **로컬 네트워크 게이트웨이 선택** 및 선택 hello 로컬 네트워크 게이트웨이 toouse 되도록 합니다. 예제에서는 **Site2**를 사용합니다.
  - **공유 키:** hello 값을 여기에 로컬 온-프레미스 VPN 장치에 사용 하는 hello 값과 일치 해야 합니다. Hello 예제에서는 'abc123' 사용 되지만 있습니다 수 (및 해야) 사용 하 여 조금 더 복잡 한 합니다. 중요 한 점은 여기에서 지정한 hello 값 hello hello VPN 장치를 구성할 때 지정한 같은 값 이어야 합니다.
  - hello에 대 한 값을 나머지 **구독**, **리소스 그룹**, 및 **위치** 고정 됩니다.

4. 클릭 **확인** toocreate 연결 합니다. 표시 *만드는 연결* hello 화면에 플래시 합니다.
5. Hello에 hello 연결을 볼 수 있습니다 **연결** hello 가상 네트워크 게이트웨이의 블레이드입니다. hello 상태 이동에서 *알 수 없는* 너무*연결*, 한 다음 너무*Succeeded*합니다.
