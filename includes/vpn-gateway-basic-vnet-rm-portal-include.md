toocreate hello Azure 포털을 사용 하 여 hello 리소스 관리자 배포 모델에서 VNet 아래 hello 단계를 따릅니다. hello 스크린 샷은 예로 제공 됩니다. 자신의 있는지 tooreplace hello 값 수입니다. 가상 네트워크 사용에 대 한 자세한 내용은 참조 hello [가상 네트워크 개요](../articles/virtual-network/virtual-networks-overview.md)합니다.

1. 브라우저에서 탐색 toohello [Azure 포털](http://portal.azure.com) 및 필요에 따라 Azure 계정으로 로그인 합니다.
2. 페이지 맨 아래에 있는 **+**를 사용하여 응용 프로그램에 Single Sign-On 할 수 있습니다. Hello에 **hello 마켓플레이스** 필드에 "가상 네트워크"를 입력 합니다. 찾을 **가상 네트워크** 에서 반환 하는 hello 목록 이동한 tooopen hello 클릭 **가상 네트워크** 페이지.

  ![Virtual Network 리소스 찾기 페이지](./media/vpn-gateway-basic-vnet-rm-portal-include/newvnetportal700.png "가상 네트워크 리소스 찾기 페이지")
3. Hello 아래 근처의 hello 가상 네트워크 페이지에서 hello **배포 모델 선택** 목록에서 선택 **리소스 관리자**, 클릭 하 고 **만들기**합니다.

  ![리소스 관리자 선택](./media/vpn-gateway-basic-vnet-rm-portal-include/resourcemanager250.png "리소스 관리자 선택")
4. Hello에 **가상 네트워크 만들기** 페이지 hello VNet 설정을 구성 합니다. Hello 필드를 입력 하는 경우 hello 빨간색 느낌표 수 녹색 확인 표시가 hello 필드에 입력 한 hello 문자는 사용할 수 있습니다. 자동으로 채워진 값이 있을 수도 있습니다. 그렇다면 자신의 hello 값을 바꿉니다. hello **가상 네트워크 만들기** 페이지에는 다음 예제와 비슷한 toohello 보입니다.

  ![가상 네트워크 만들기 페이지](./media/vpn-gateway-basic-vnet-rm-portal-include/createvnet300.png "가상 네트워크 만들기 페이지")
5. **이름**: 가상 네트워크에 대 한 hello 이름을 입력 합니다.
6. **주소 공간**: hello 주소 공간을 입력 합니다. 여러 주소 공간 tooadd를 설정한 경우 첫 번째 주소 공간을 추가 합니다. 나중에 hello VNet을 만든 후 추가 주소 공간을 추가할 수 있습니다.
7. **서브넷 이름**: hello 서브넷 이름 및 서브넷 주소 범위를 추가 합니다. 나중에 hello VNet을 만든 후 서브넷을 더 추가할 수 있습니다.
8. **구독**: 구독 나열 된 해당 hello 올바른 hello는 확인 합니다. Hello 드롭 다운을 사용 하 여 구독을 변경할 수 있습니다.
9. **리소스 그룹**: 기존 리소스 그룹을 선택하거나 새 리소스 그룹의 이름을 입력하여 새로 만듭니다. 새 그룹을 만드는 경우 tooyour에 따라 이름 hello 리소스 그룹 구성 값을 계획 합니다. 리소스 그룹에 대한 자세한 내용은 [Azure Resource Manager 개요](../articles/azure-resource-manager/resource-group-overview.md#resource-groups)를 참조하세요.
10. **위치**: VNet에 대 한 hello 위치를 선택 합니다. hello 위치 toothis VNet을 배포 하는 hello 리소스 상주할 위치를 결정 합니다.
11. 선택 **Pin toodashboard** toobe 수 toofind hello 대시보드에 쉽게 VNet을 클릭 하는 경우 **만들기**합니다.

 ![Pin toodashboard](./media/vpn-gateway-basic-vnet-rm-portal-include/pintodashboard150.png "pin toodashboard")
12. 클릭 한 후 **만들기**, VNet의 hello 진행 상태를 나타내는 대시보드 타일을 표시 됩니다. hello와 hello 타일 변경 사항이 VNet은 만드는 중입니다.

  ![가상 네트워크 타일 만들기](./media/vpn-gateway-basic-vnet-rm-portal-include/deploying150.png "Creating virtual network tile")