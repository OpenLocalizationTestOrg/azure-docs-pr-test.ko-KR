toocreate hello Azure 포털을 사용 하 여 hello 리소스 관리자 배포 모델에서 VNet 아래 hello 단계를 따릅니다. 사용 하 여 hello [예제 값](#values) 자습서도 다음이 단계를 사용 하는 경우. 자습서로 다음이 단계를 수행 하지 않습니다 수 자신의 있는지 tooreplace hello 값. 가상 네트워크 사용에 대 한 자세한 내용은 참조 hello [가상 네트워크 개요](../articles/virtual-network/virtual-networks-overview.md)합니다.

1. 브라우저에서 탐색 toohello [Azure 포털](http://portal.azure.com) Azure 계정으로 로그인 합니다.
2. **새로 만들기**를 클릭합니다. Hello에 **hello 마켓플레이스** 필드 ' 가상 네트워크 '를 입력 합니다. 찾을 **가상 네트워크** 에서 반환 하는 hello 목록 이동한 tooopen hello 클릭 **가상 네트워크** 블레이드입니다.
3. Hello 아래 근처의 hello에서 hello 가상 네트워크 블레이드 **배포 모델 선택** 목록에서 선택 **리소스 관리자**, 클릭 하 고 **만들기**합니다. Hello '가상 네트워크 만들기' 블레이드가 열립니다.

    ![가상 네트워크 블레이드 만들기](./media/vpn-gateway-basic-vnet-s2s-rm-portal-include/createvnet.png "Create virtual network blade")
4. Hello에 **가상 네트워크 만들기** 블레이드에서 hello VNet 설정을 구성 합니다. Hello 필드를 입력 하는 경우 hello 빨간색 느낌표 수 녹색 확인 표시가 hello 필드에 입력 한 hello 문자는 사용할 수 있습니다.

  - **이름**: 가상 네트워크에 대 한 hello 이름을 입력 합니다. 이 예제에서는 TestVNet1을 사용합니다.
  - **주소 공간**: hello 주소 공간을 입력 합니다. 여러 주소 공간 tooadd를 설정한 경우 첫 번째 주소 공간을 추가 합니다. 나중에 hello VNet을 만든 후 추가 주소 공간을 추가할 수 있습니다. 온-프레미스 위치에 대 한 hello 주소 공간과 겹치지 않는 지정 하는 해당 hello 주소 공간이 있는지 확인 합니다.
  - **서브넷 이름**: hello 첫 번째 서브넷 이름 및 서브넷 주소 범위를 추가 합니다. 이 VNet을 만든 후 서브넷을 더 및 hello 게이트웨이 서브넷을 나중에 추가할 수 있습니다. 
  - **구독**: 나열 된 hello 구독 올바른 hello가 있는지 확인 합니다. Hello 드롭 다운을 사용 하 여 구독을 변경할 수 있습니다.
  - **리소스 그룹**: 기존 리소스 그룹을 선택하거나 새 리소스 그룹의 이름을 입력하여 새로 만듭니다. 새 그룹을 만드는 경우 tooyour에 따라 이름 hello 리소스 그룹 구성 값을 계획 합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.
  - **위치**: VNet에 대 한 hello 위치를 선택 합니다. hello 위치 toothis VNet을 배포 하는 hello 리소스 상주할 위치를 결정 합니다.

5. 선택 **Pin toodashboard** toobe 수 toofind hello 대시보드에 쉽게 VNet을 클릭 하는 경우 **만들기**합니다. 클릭 한 후 **만들기**, VNet의 hello 진행 상태를 나타내는 대시보드 타일을 표시 됩니다. hello와 hello 타일 변경 사항이 VNet은 만드는 중입니다.
