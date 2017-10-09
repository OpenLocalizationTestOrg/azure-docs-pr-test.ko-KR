1. Hello hello 포털 페이지의 왼쪽, 클릭  **+**  검색에 ' 가상 네트워크 게이트웨이 '를 입력 합니다. **결과**에서 **가상 네트워크 게이트웨이**를 찾아 클릭합니다.
2. Hello '가상 네트워크 게이트웨이' 블레이드의 hello 아래쪽 클릭 **만들기**합니다. Hello 열립니다 **가상 네트워크 게이트웨이 만들기** 블레이드입니다.

    ![가상 네트워크 게이트웨이 블레이드 필드 만들기](./media/vpn-gateway-add-gw-s2s-rm-portal-include/vnet_gw.png "새로운 게이트웨이")

3. Hello에 **가상 네트워크 게이트웨이 만들기** 블레이드를 가상 네트워크 게이트웨이에 대 한 hello 값을 지정 합니다.

  - **이름**: 게이트웨이 이름을 지정합니다. 이 게이트웨이 서브넷 이름 지정과 동일 hello 없습니다. 만들려는 hello 게이트웨이 개체의 hello 이름의 것입니다.
  - **게이트웨이 유형**: **VPN**을 선택합니다. VPN 게이트웨이 hello 가상 네트워크 게이트웨이 유형을 사용 하 여 **VPN**합니다. 
  - **VPN 유형**: 구성에 대해 지정 된 hello VPN 유형을 선택 합니다. 대부분의 구성에는 경로 기반 VPN 유형이 필요합니다.
  - **SKU**: hello 드롭다운에서 선택 hello 게이트웨이 SKU입니다. hello 드롭다운에 나열 된 hello Sku hello 선택한 VPN 종류에 따라 다릅니다. 게이트웨이 SKU에 대한 자세한 내용은 [게이트웨이 SKU](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#gwsku)를 참조하세요.
  - **위치**: tooscroll toosee 위치를 할 수 있습니다. Hello 조정 **위치** 가상 네트워크가 있는 toopoint toohello 위치 필드입니다. Hello 위치 toohello 지역 가상 네트워크가 있는 위치를 가리키지 않습니다, 경우 hello 가상 네트워크에에서 나타나지 않습니다 hello 다음 단계 드롭다운 '가상 네트워크를 선택 합니다.'.
  - **가상 네트워크**: hello 가상 네트워크 toowhich 선택 tooadd이이 게이트웨이 선택 합니다. 클릭 **가상 네트워크** tooopen hello '가상 네트워크를 선택 합니다.' 블레이드입니다. Hello VNet을 선택 합니다. VNet 보이지 않으면 hello 위치 필드 toohello 지역 가상 네트워크의 위치를 가리키는 가리키고 있는지 확인 합니다.
  - **공용 IP 주소**: hello '공용 IP 주소 만들기' 블레이드 공용 IP 주소 개체를 만듭니다. hello 공용 IP 주소는 hello VPN 게이트웨이 만들 때 동적으로 할당 됩니다. 현재 VPN Gateway는 *동적* 공용 IP 주소 할당만 지원합니다. 그러나 hello IP 주소가 변경 tooyour VPN 게이트웨이에 할당 된 이후에이 아닙니다. hello 유일한 시간 hello 공용 IP 주소 변경 내용을 게이트웨이 hello 때 삭제 되어 다시 만들어집니다. VPN Gateway의 크기 조정, 다시 설정 또는 기타 내부 유지 관리/업그레이드 시에는 변경되지 않습니다.

    - 먼저, 클릭 **공용 IP 주소** tooopen 블레이드 '공용 IP 주소 선택' hello 한 다음 클릭 **+ 새로 만들기** tooopen hello '공용 IP 주소 만들기' 블레이드입니다.
    - 다음으로 입력 한 **이름** 공용 IP 주소에 대해 클릭 **확인** 에 hello이 블레이드 toosave 맨 변경 내용을 합니다.

      ![공용 IP 만들기](./media/vpn-gateway-add-gw-s2s-rm-portal-include/pip.png "PIP 만들기")

4. Hello 설정을 확인 합니다. 선택할 수 있습니다 **Pin toodashboard** hello hello 대시보드에서 사용자 게이트웨이 tooappear 하려는 경우 hello 블레이드 맨 아래에 있습니다. 
5. 클릭 **만들기** toobegin hello VPN 게이트웨이 만들기. hello 표시 하 고 hello 설정의 유효성을 검사 합니다 "배포 가상 네트워크 게이트웨이" hello 대시보드에서 타일입니다. 한 게이트웨이 만드는 too45 분 정도 걸릴 수 있습니다. 포털 페이지 toosee hello 완료 상태가 toorefresh를 할 수 있습니다.

Hello 게이트웨이 만든 후에 hello hello 포털에서 가상 네트워크를 살펴보면 tooit 할당 된 hello IP 주소를 봅니다. hello 게이트웨이 연결된 된 장치로 표시 됩니다. 자세한 내용은 연결 된 hello 장치 (가상 네트워크 게이트웨이) tooview를 클릭할 수 있습니다.
