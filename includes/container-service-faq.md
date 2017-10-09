# <a name="container-service-frequently-asked-questions"></a>Container Service 질문과 대답

## <a name="orchestrators"></a>오케스트레이터

### <a name="which-container-orchestrators-do-you-support-on-azure-container-service"></a>Azure Container Service에 어떤 컨테이너 오케스트레이터가 지원되나요? 

오픈 소스 DC/OS, Docker Swarm 및 Kubernetes가 지원됩니다. 자세한 내용은 참조 hello [개요](../articles/container-service/kubernetes/container-service-intro-kubernetes.md)합니다.
 
### <a name="do-you-support-docker-swarm-mode"></a>Docker Swarm 모드가 지원되나요? 

현재 웜 모드는 지원 되지 않지만 hello 서비스 로드맵 켜져 있습니다. 

### <a name="does-azure-container-service-support-windows-containers"></a>Azure Container Service에 Windows 컨테이너가 지원되나요?  

현재 Linux 컨테이너는 모든 오케스트레이터에 지원됩니다. Kubernetes를 통한 Windows 컨테이너에 대한 지원은 미리 보기 상태입니다.

### <a name="do-you-recommend-a-specific-orchestrator-in-azure-container-service"></a>Azure Container Service에 권장되는 특정 오케스트레이터가 있나요? 
일반적으로 특정 오케스트레이터가 권장되지는 않습니다. 지원 되는 hello orchestrators 중 하나가 지정 된 경험이 있다면 Azure 컨테이너 서비스에서 해당 환경을 적용할 수 있습니다. 하지만 데이터 경향에 따르면 DC/OS는 빅 데이터 및 IoT 워크로드에 대해 성능이 입증되었고 Kubernetes는 클라우드 네이티브 워크로드에 적합하며 Docker Swarm은 Docker 도구와의 통합 및 학습이 쉬운 것으로 알려져 있습니다.

시나리오에 따라 다른 Azure 서비스를 사용하여 사용자 지정 컨테이너 솔루션을 구축하고 관리할 수도 있습니다. 이러한 서비스에는 [Virtual Machines](../articles/virtual-machines/linux/overview.md), [Service Fabric](../articles/service-fabric/service-fabric-overview.md), [Web Apps](../articles/app-service-web/app-service-web-overview.md) 및 [Batch](../articles/batch/batch-technical-overview.md)가 있습니다.  

### <a name="what-is-hello-difference-between-azure-container-service-and-acs-engine"></a>Azure 컨테이너 서비스 및 ACS 엔진의 hello 차이점은 무엇입니까? 
Azure 컨테이너 서비스는 hello Azure 포털, Azure 명령줄 도구 및 Azure Api의 기능을 통해 SLA 지원 Azure 서비스입니다. hello 서비스 구현 tooquickly 수 있도록 하 고 선택한 구성 항목의 상대적으로 적은 번호로 표준 컨테이너 오케스트레이션 도구를 실행 하는 클러스터를 관리 합니다. 

[ACS 엔진](http://github.com/Azure/acs-engine) 모든 수준에서 전원 사용자 toocustomize hello 클러스터 구성을 사용 하도록 설정 하는 오픈 소스 프로젝트입니다. 이 기능은 tooalter hello 구성의 인프라와 소프트웨어를 모두 ACS 엔진에 대 한 SLA를 제공 하지는 제공 의미 합니다. 지원 공식 Microsoft 채널 대신 GitHub의 오픈 소스 프로젝트 hello 통해 처리 됩니다. 

## <a name="cluster-management"></a>클러스터 관리

### <a name="how-do-i-create-ssh-keys-for-my-cluster"></a>클러스터의 SSH 키는 어떻게 만드나요?

표준 도구를 클러스터에 대 한 hello Linux 가상 컴퓨터에 대 한 인증에 대 한 사용자 운영 체제 toocreate SSH RSA 공개 및 개인 키 쌍에서 사용할 수 있습니다. 단계를 참조 hello [Osx 및 Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) 또는 [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) 지침. 

사용 하는 경우 [Azure CLI 2.0 명령은](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy 컨테이너는 클러스터 서비스, SSH 키 수 자동으로 생성 될 클러스터에 대 한 합니다.

### <a name="how-do-i-create-a-service-principal-for-my-kubernetes-cluster"></a>Kubernetes 클러스터에 대한 서비스 주체는 어떻게 만드나요?

Azure Active Directory 서비스 보안 주체 ID 및 암호가 필요한 toocreate Azure 컨테이너 서비스의 Kubernetes 클러스터 됩니다. 자세한 내용은 참조 [Kubernetes 클러스터에 대 한 hello 서비스 사용자에 대 한](../articles/container-service/kubernetes/container-service-kubernetes-service-principal.md)합니다.

사용 하는 경우 [Azure CLI 2.0 명령은](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) toodeploy는 Kubernetes 클러스터, 서비스를 클러스터에 대해 사용자 자격 증명을 자동으로 생성 됩니다.

### <a name="how-large-a-cluster-can-i-create"></a>얼마나 큰 클러스터를 만들 수 있나요?
1, 3 또는 5개의 마스터 노드가 있는 클러스터를 만들 수 있습니다. Too100 에이전트 노드를 선택할 수 있습니다.

> [!IMPORTANT]
> 더 큰 클러스터 및 hello 해당 노드에 대 한 선택 하는 VM 크기에 따라 구독에서 tooincrease hello 코어 할당량을 할 수 있습니다. 할당량 증가 열기 toorequest는 [온라인 고객 지원 요청](../articles/azure-supportability/how-to-create-azure-support-request.md) 비용 없이 합니다. [Azure 무료 계정](https://azure.microsoft.com/free/)을 사용하는 경우, 제한된 수의 Azure 계산 코어만 사용할 수 있습니다.
> 

### <a name="how-do-i-increase-hello-number-of-masters-after-a-cluster-is-created"></a>클러스터를 만든 후 마스터 hello 수가 늘리려면 어떻게 해야 합니까? 
Hello 클러스터를 만든 후에 마스터 hello 수가 고정 되어 있고 변경할 수 없습니다. Hello 클러스터의 hello 만드는 동안 이상적으로 고가용성을 위해 여러 마스터를 선택 해야 합니다.

### <a name="how-do-i-increase-hello-number-of-agents-after-a-cluster-is-created"></a>클러스터를 만든 후 에이전트 수가 hello 늘리려면 어떻게 해야 합니까? 
Hello Azure 포털 또는 명령줄 도구를 사용 하 여 hello 클러스터의 에이전트의 hello 수를 확장할 수 있습니다. [Azure Container Service 클러스터 규모 조정](../articles/container-service/kubernetes/container-service-scale.md)을 참조하세요.

### <a name="what-are-hello-urls-of-my-masters-and-agents"></a>내 마스터 및 에이전트의 hello Url은 무엇입니까? 
hello Url Azure 컨테이너 서비스의 리소스 기반 hello로 클러스터의 DNS 이름 접두사를 제공 하 고 hello 이름 hello 배포에 대해 선택한 Azure 지역입니다. 예를 들어 hello hello 마스터 노드의 정규화 된 도메인 이름 (FQDN)이이 폼입니다.

``` 
DNSnamePrefix.AzureRegion.cloudapp.azure.net
```

Hello Azure 포털, Azure 리소스 탐색기 hello 또는 다른 Azure 도구에서 클러스터에 대해 자주 사용 되는 Url을 찾을 수 있습니다.

### <a name="how-do-i-tell-which-orchestrator-version-is-running-in-my-cluster"></a>내 클러스터에 실행 중인 오케스트레이터 버전을 어떻게 확인하나요?

* DC/OS: hello 참조 [Mesosphere 설명서](https://support.mesosphere.com/hc/en-us/articles/207719793-How-to-get-the-DCOS-version-from-the-command-line-)
* Docker Swarm: `docker version` 실행
* Kubernetes: `kubectl version` 실행

### <a name="how-do-i-upgrade-hello-orchestrator-after-deployment"></a>배포 후 hello orchestrator를 업그레이드 하려면 어떻게 합니까?

현재 Azure 컨테이너 서비스 클러스터에 배포 된 hello orchestrator의 도구 tooupgrade hello 버전을 제공 하지 않습니다. Container Service에서 새로운 버전을 지원하는 경우 새 클러스터를 배포할 수 있습니다. 또 다른 옵션은 사용할 수 있는 위치에 클러스터 tooupgrade 않으면 toouse orchestrator 관련 도구입니다. 예를 들어 [DC/OS 업그레이드](https://dcos.io/docs/1.8/administration/upgrading/)를 참조하세요.
 
### <a name="where-do-i-find-hello-ssh-connection-string-toomy-cluster"></a>Hello SSH 연결 문자열 toomy 클러스터 어디에 있습니까?

Hello Azure 포털 또는 Azure 명령줄 도구를 사용 하 여 hello 연결 문자열을 찾을 수 있습니다. 

1. Hello 포털에서 hello 클러스터 배포에 대 한 toohello 리소스 그룹을 이동 합니다.  

2. 클릭 **개요** hello 링크를 클릭 하 고 **배포** 아래 **Essentials**합니다. 

3. Hello에 **배포 기록을** 블레이드에서로 이름을 시작 하는 hello 배포를 클릭 **microsoft acs** 배포 날짜 옵니다. 예: microsoft-acs-201701310000.  

4. Hello에 **요약** 페이지의 **출력**, 여러 클러스터 링크가 제공 됩니다. **SSHMaster0** 는 SSH 연결 문자열 toohello 첫 번째 마스터 컨테이너 서비스 클러스터에 제공 합니다. 

에서 설명한 대로 Azure tools toofind hello hello 마스터의 FQDN을 사용할 수도 있습니다. Toohello 마스터 hello FQDN hello 마스터 및 hello 클러스터를 만들 때 지정한 hello 사용자 이름을 사용 하 여 SSH 연결을 확인 합니다. 예:

```bash
ssh userName@masterFQDN –A –p 22 
```

자세한 내용은 참조 [연결 tooan Azure 컨테이너 서비스 클러스터](../articles/container-service/kubernetes/container-service-connect.md)합니다.

## <a name="next-steps"></a>다음 단계

* Azure Container Service에 대해 [자세히 알아보세요](../articles/container-service/kubernetes/container-service-intro-kubernetes.md).
* Hello를 사용 하 여 컨테이너 서비스 클러스터 배포 [포털](../articles/container-service/dcos-swarm/container-service-deployment.md) 또는 [Azure CLI 2.0](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)합니다.
