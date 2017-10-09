

![독립 실행형 클라우드 서비스의 가상 컴퓨터](./media/virtual-machines-common-classic-connect-vms/CloudServiceExample.png)

가상 네트워크의 가상 컴퓨터를 배치 하는 경우 개수 클라우드 서비스에 대 한 toouse 원하는 부하 분산 및 가용성 집합을 결정할 수 있습니다. Hello 가상 컴퓨터를 구성할 수는 또한 hello의 서브넷에서 같은 방식으로 온-프레미스 네트워크 및 가상 네트워크 tooyour hello 연결 온-프레미스 네트워크입니다. 예를 들면 다음과 같습니다.

![가상 네트워크의 가상 컴퓨터](./media/virtual-machines-common-classic-connect-vms/VirtualNetworkExample.png)

가상 네트워크는 hello Azure의 방식으로 tooconnect 가상 컴퓨터를 권장 합니다. 가장 좋은 방법은 hello tooconfigure 별도 클라우드 서비스에서 응용 프로그램의 각 계층은 합니다. 그러나 해야 toocombine 일부 가상 컴퓨터 hello에 여러 응용 프로그램 계층에서 동일한 클라우드 서비스 tooremain hello 최대 구독 당 200 클라우드 서비스 내에서. tooreview이 및 다른 제한을 참조 [Azure 구독 및 서비스 제한, 할당량 및 제약 조건](../articles/azure-subscription-service-limits.md)합니다.

## <a name="connect-vms-in-a-virtual-network"></a>가상 네트워크에서 VM 연결
가상 네트워크의 가상 컴퓨터를 tooconnect:

1. Hello에 hello 가상 네트워크 만들기 [Azure 포털](../articles/virtual-network/virtual-networks-create-vnet-classic-pportal.md) '클래식 배포'를 지정 합니다.
2. Hello 집합 배포 tooreflect에 대 한 클라우드 서비스의 가용성 집합에 대 한 디자인 만들고 부하 분산 합니다. Hello Azure 포털에서에서 클릭 **새로 만들기 > 계산 > 클라우드 서비스** 각 클라우드 서비스에 대 한 합니다.

  Hello 클라우드 서비스 정보를 입력으로 선택 동일 hello _리소스 그룹_ hello 가상 네트워크와 함께 사용 합니다.

3. toocreate 각각의 새 가상 컴퓨터를 클릭 **새로 만들기 > 계산**, 선택 hello hello에서 적절 한 VM 이미지 다음 **추천 앱**합니다.

  Hello VM에서에서 **기본 사항** 블레이드에서 선택 동일 hello _리소스 그룹_ hello 가상 네트워크와 함께 사용 합니다.

  ![VNet을 사용하는 경우 VM 기본 블레이드](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_VN.png)

4. 작성할 때 VM hello 양식에 **설정**, 올바른 hello 선택 _클라우드 서비스_ 또는 _가상 네트워크_ hello VM에 대 한 합니다.

  Azure는 hello 다른 선택에 따라 항목을 선택 합니다.

  ![VNet을 사용하는 경우 VM 설정 블레이드](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_VN.png)


## <a name="connect-vms-in-a-standalone-cloud-service"></a>독립 실행형 클라우드 서비스에서 VM 연결
독립 실행형 클라우드 서비스에서 tooconnect 가상 컴퓨터:

1. Hello에 hello 클라우드 서비스를 만들 [Azure 포털](http://portal.azure.com)합니다. **새로 만들기 > 계산 > 클라우드 서비스**를 클릭합니다. 또는 첫 번째 가상 컴퓨터를 만들 때 배포에 대 한 hello 클라우드 서비스를 만들 수 있습니다.
2. Hello 가상 컴퓨터를 만들 때 hello hello 클라우드 서비스와 함께 사용 되는 동일한 리소스 그룹을 선택 합니다.

  ![가상 컴퓨터 tooan 기존 클라우드 서비스를 추가 합니다.](./media/virtual-machines-common-classic-connect-vms/CreateVM_Basics_SA.png)

3.  Hello VM 세부 정보를 입력 하는 대로 hello 첫 번째 단계에서 만든 클라우드 서비스의 hello 이름을 선택 합니다.

  ![가상 컴퓨터에 대한 클라우드 서비스 선택](./media/virtual-machines-common-classic-connect-vms/CreateVM_Settings_SA.png)
