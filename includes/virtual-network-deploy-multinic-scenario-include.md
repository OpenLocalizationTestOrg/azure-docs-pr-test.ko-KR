## <a name="scenario"></a>시나리오
이 문서는 특정 시나리오에서 VM에 다중 NIC를 사용하는 배포를 살펴봅니다. 이 시나리오에는 Azure에 호스트되는 2계층 IaaS 워크로드가 있습니다. 각 계층은 가상 네트워크(VNet)의 자체 서브넷에 배포됩니다. 고가용성을 위해 설정 하는 부하 분산 장치에서 함께 그룹화 하는 여러 웹 서버, hello 프런트 엔드 계층으로 구성 됩니다. 여러 데이터베이스 서버 hello 백 엔드 계층으로 구성 됩니다. 이러한 데이터베이스 서버는 두 개의 nic가 각, 데이터베이스 액세스에 대 한 함께 배포, 관리에 대 한 다른 hello 합니다. 또한 hello 시나리오 수 있는 트래픽에 tooeach 서브넷과 NIC hello 배포에서 네트워크 보안 그룹 (Nsg) toocontrol 포함 합니다. 아래 hello 그림 hello이이 시나리오의 기본 아키텍처를 보여 줍니다.  

![MultiNIC 시나리오](./media/virtual-network-deploy-multinic-scenario-include/Figure1.png)

