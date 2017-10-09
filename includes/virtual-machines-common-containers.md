Azure 클라우드 솔루션은 가상 컴퓨터(물리적 컴퓨터 하드웨어의 에뮬레이션)에 구축되어 물리적 하드웨어보다 소프트웨어 배포를 빠르게 패키징하고 리소스 통합을 훨씬 원활하게 수행할 수 있습니다. [Docker](https://www.docker.com) hello 및 컨테이너 docker 생태계는 획기적으로 확장 된 hello 방법으로 개발, 배송, 및 분산된 소프트웨어를 관리할 수 있습니다. Hello 호스트 VM에서에서 격리 된 컨테이너에서 응용 프로그램 코드 및 기타 컨테이너에서 hello 동일한 VM입니다. 이 격리로 인해 개발 및 배포 유연성이 증가합니다.

Azure는 hello 다음 Docker 값을 제공 합니다.

* [많은](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) [다른](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) 상황 toosuit 컨테이너에 대 한 방법으로 toocreate Docker 호스트
* hello [Azure 컨테이너 서비스](https://azure.microsoft.com/documentation/services/container-service/) 같은 orchestrators를 사용 하 여 컨테이너 호스트의 클러스터를 만듭니다 **마라톤** 및 **swarm**합니다.
* [Azure 리소스 관리자](../articles/azure-resource-manager/resource-group-overview.md) 및 [리소스 그룹 템플릿](../articles/resource-group-authoring-templates.md) toosimplify 배포 및 복잡 한 분산된 응용 프로그램 업데이트
* 여러 독점 및 공개 소스 구성 관리 도구와 통합

Vm 및 Linux를 프로그래밍 방식으로 만들 수 있기 때문에 및 컨테이너 Azure에서 사용할 수도 있습니다 VM 및 컨테이너 *오케스트레이션* 가상 컴퓨터 (Vm) 및 두 Linux 내부의 toodeploy 응용 프로그램의 toocreate 그룹 도구 컨테이너 및 지금 [Windows 컨테이너](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)합니다.

이 문서 뿐만 아니라 높은 수준에서 이러한 개념을 설명, 자습서, 링크 toomore 정보의 톤도 포함 되어 및 제품 관련 Azure에서 toocontainer와 클러스터 사용 합니다. 이 모든, 확인 하 고 hello 링크 원하는 경우에 있는 것 바로 여기 [컨테이너 작업에 대 한 도구](#tools-for-working-with-azure-vms-and-containers)합니다.

## <a name="hello-difference-between-virtual-machines-and-containers"></a>가상 컴퓨터와 컨테이너 간의 hello 차이
가상 컴퓨터는 [하이퍼바이저](http://en.wikipedia.org/wiki/Hypervisor)가 제공하는 독립된 하드웨어 가상화 환경 내에서 실행됩니다. Azure의 hello [가상 컴퓨터](https://azure.microsoft.com/services/virtual-machines/) 있습니다에 대 한 핸들을 하는 모든 서비스: hello 운영 체제를 선택 하 고 구성 하 여 가상 컴퓨터를 만들 &mdash;또는 사용자 지정 VM 이미지를 업로드 하 여 합니다. 가상 컴퓨터는 여기서, "전투 확정" 기술 이며 많은 도구가 포함 되어 사용 가능한 toomanage hello 운영 체제 및 응용 프로그램입니다.  VM에서 응용 프로그램 hello 호스트 운영 체제에서에서 숨겨집니다. Hello 관점에서 응용 프로그램 또는 VM에는 사용자, VM hello toobe 자치 물리적 컴퓨터는 표시 됩니다.

[Linux 컨테이너](http://en.wikipedia.org/wiki/LXC) 만들어지고 docker 도구를 사용 하 여 호스트 된 하이퍼바이저 tooprovide 격리를 사용 하지 않습니다. 컨테이너를 hello 컨테이너 호스트 프로세스 및 hello Linux 커널 tooexpose toohello 컨테이너의 파일 시스템 격리 기능, 해당 응용 프로그램, 특정 커널 기능 및 자체 격리 된 파일 시스템을 사용합니다. Hello 관점에서 컨테이너 내에서 실행 되는 응용 프로그램의, hello 컨테이너 고유 OS 인스턴스 toobe 나타납니다. 컨테이너 내 앱에서는 해당 컨테이너 외부에 있는 프로세스나 기타 리소스를 볼 수 없습니다.

Docker 컨테이너에 사용되는 리소스는 VM에서 사용하는 것보다 훨씬 적습니다. Docker 컨테이너 응용 프로그램 격리 및 실행 모델을 hello Docker 호스트의 커널은 hello를 공유 하지 않습니다는 사용 합니다. hello 컨테이너에 훨씬 더 낮은 디스크 사용 공간의 포함 되지 않으면 전체 OS hello 합니다. 시작 시간과 필수 디스크 공간은 VM에 비해 훨씬 낮습니다.
Windows 컨테이너 Windows에서 실행 되는 앱에 대 한 hello Linux 컨테이너와 같은 장점을 제공 합니다. Windows 컨테이너는 hello Docker 이미지 형식 및 Docker API를 지원 하지만 PowerShell을 사용 하 여 관리할 수도 수 있습니다. 두 개의 컨테이너 런타임을 Windows 컨테이너, Windows Server 컨테이너 및 Hyper-V 컨테이너에서 사용할 수 있습니다. Hyper-V 컨테이너는 매우 최적화된 VM에서 각 컨테이너를 호스트하여 추가 격리 계층을 제공합니다. Windows 컨테이너에 대 한 자세한 참조 toolearn [Windows 컨테이너에 대 한](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)합니다. azure에서 Windows 컨테이너 시작 tooget 너무 방법을 알아보려면[Azure 컨테이너 서비스 클러스터를 배포할](../articles/container-service/dcos-swarm/container-service-deployment.md)합니다.

## <a name="what-are-containers-good-for"></a>컨테이너의 이점

컨테이너는 다음을 향상시킬 수 있습니다.

* hello 속도 응용 프로그램 코드를 개발 하 고 광범위 하 게 공유 수 있습니다.
* hello 속도 신뢰 응용 프로그램을 테스트.
* hello 속도 신뢰 응용 프로그램을 배포할 수 있습니다

컨테이너는 컨테이너 호스트&mdash;운영 체제, 그리고 Azure(Azure Virtual Machine)에서 실행됩니다. 컨테이너의 hello 개념을 이미 선호, 여전히 거 tooneed hello 컨테이너 호스트 VM 인프라 했지만 hello 이점은 컨테이너 중요 하지 않은 경우에 어떤 VM에서 실행 (하지만 Linux 또는 Windows hello 컨테이너의가 있는지 여부 실행 환경에서 수, 중요 한 예를 들어).


## <a name="what-are-containers-good-for"></a>컨테이너의 이점
여러 가지 원인에 매우 유용 하지만 권장&mdash;마찬가지로 [Azure 클라우드 서비스](https://azure.microsoft.com/services/cloud-services/) 및 [Azure 서비스 패브릭](../articles/service-fabric/service-fabric-overview.md)&mdash;hello 단일 서비스, 마이크로 서비스 지향 만들기 분산된 응용 프로그램, 응용 프로그램에서 설계는 대신 더 큰, 더욱 강력 하 게 결합 된 구성 요소에 더 많은 소형, 구성 가능 부품에 기반 합니다.

특히 Azure와 같은 공용 클라우드 환경에서는 VM이 필요할 때 언제 어디서나 가져다 쓸 수 있기 때문에 더욱 그 진가를 발합니다. 격리, 신속한 배포, 오케스트레이션 도구를 쉽게 가져와 사용할 수 있을 뿐만 아니라 더욱 효율적으로 응용 프로그램 인프라를 결정할 수 있습니다.

예를 들어, 접속 규모가 대단히 큰 분산형 응용 프로그램 배포를 위해 9개의 대규모 Azure VM을 구성한다고 가정해 보겠습니다. 컨테이너에서이 응용 프로그램의 hello 구성 요소를 배포할 수 있는 경우 4 Vm 으로만 수 toouse 될 수도 있으며 중복 및 부하 분산에 대 한 20 컨테이너 내부의 응용 프로그램 구성 요소를 배포할 수 있습니다.

이것은 예 시일 뿐, 있지만 시나리오에서이 작업을 수행할 수 있습니다, 더 많은 Azure Vm이 아닌 더 많은 컨테이너와 함께 toousage 스파이크를 조정 하 고 이전 보다 훨씬 더 효율적으로 전체 CPU 부하를 남은 hello를 사용 하 여 수 있습니다.

또한 tooa microservices 접근 방식을; 해야 하지 않는 시나리오도 있습니다. 여부 microservices 및 컨테이너를 통해 수 가장 잘 알게 됩니다.

### <a name="container-benefits-for-developers"></a>컨테이너가 개발자에게 주는 이점
일반적으로 컨테이너 기술은 단계를 앞으로 이동 하지만 혜택이 있으며 보다 구체적인도 쉽게 toosee는 것입니다. Docker 컨테이너의 hello 예제를 살펴보겠습니다. 이 항목은 하지에 대해 자세히 알아보기 밀접 하 게 Docker 지금 바로 (읽기 [Docker 란?](https://www.docker.com/whatisdocker/) 해당 스토리에 대 한 또는 [wikipedia](http://wikipedia.org/wiki/Docker_%28software%29)), Docker 및 ecosystem 제공 되는 큰 혜택 tooboth 개발자 및 IT 전문가입니다.

개발자가 만들므로 무엇 보다 쉽게 Windows와 Linux 컨테이너를 사용 하 여 tooDocker 컨테이너를 신속 하 게 수행 합니다.

* 간단 하 고 증분 명령을 toocreate 쉽게 toodeploy 있는 고정 된 이미지를 사용할 수 있습니다. 및 dockerfile을 사용 하 여 해당 이미지를 작성을 자동화할 수 있습니다.
* 이러한 이미지를 사용 하 여 쉽게 단순, 공유할 수 [git](https://git-scm.com/)-스타일 밀어넣기 및 끌어오기 명령을 너무[공용](https://registry.hub.docker.com/) 또는 [개인 docker 레지스트리](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* 또한 컴퓨터가 아닌 격리된 응용 프로그램 구성 요소를 활용하고
* Docker 컨테이너와 다양한 기본 이미지들을 잘 다룰 수 있는 수많은 도구를 사용할 수 있습니다

### <a name="container-benefits-for-operations-and-it-professionals"></a>컨테이너가 운영 및 IT 전문가에게 주는 이점
IT 운영 전문가 컨테이너와 가상 컴퓨터의 hello 조합에서 이점을 얻을 수 있습니다.

* 컨테이너에서 실행되는 서비스는 VM 호스트 실행 환경에서 격리됩니다.
* 컨테이너 내 코드는 동일하게 인증됩니다
* 컨테이너 내 서비스는 개발, 테스트, 프로덕션 환경을 가리지 않고 신속하게 시작, 중지, 이동할 수 있습니다

이러한과 같은 기능&mdash;더 많은 요소가 및&mdash;전문 정보 기술 조직 있는 hello 작업 맞춤 리소스의 설정 된 회사, 자극&mdash;순수 처리 능력을 포함 하 여&mdash; toohello 작업 필요한 toonot 사업을 유지 하지만 고객 만족도 높일 및만 도달 합니다. 중소기업, Isv 및 시작이 hello 정확히 동일한 요구 사항이 있지만 설명 하 고 다르게 합니다.

## <a name="what-are-virtual-machines-good-for"></a>가상 컴퓨터의 이점
가상 컴퓨터 클라우드 컴퓨팅의 hello 백본을 제공 하 고는 변경 되지 않습니다. 가상 컴퓨터 보다 느리게 시작 합니다. 큰 디스크 공간을 있고 매핑되지 않는 직접 tooa microservices 아키텍처를 하는 경우 반드시 필요한 것 매우 중요 한 이점:

1. 기본적으로 호스트 컴퓨터에 훨씬 더 강력한 기본 보안 기능 제공
2. 주요 OS 및 응용 프로그램 구성 지원
3. 명령 및 제어에 장기간 사용할 수 있는 도구 환경 제공
4. Hello 실행 toohost 컨테이너 환경 제공

hello 마지막 항목은 중요, 포함 된 응용 프로그램을 여전히 필요로 하므로 특정 운영 체제 및 CPU 종류에 따라 hello 호출 hello 응용 프로그램을 만듭니다. 중요 한 tooremember toodeploy; 원하는 hello 응용 프로그램을 포함 하기 때문에 Vm에 컨테이너를 설치 하는 것이 컨테이너는 Vm 또는 운영 체제에 대 한 대체 되지 않습니다.

## <a name="high-level-feature-comparison-of-vms-and-containers"></a>VM과 컨테이너의 고급 기능 비교
hello 다음 표에서 설명에 매우 높은 수준 hello 종류의 기능 차이&mdash;많은 추가 작업 없이&mdash;컨테이너 Vm 및 Linux 사이 존재 합니다. Note 일부 기능이 필요한 응용 프로그램에 바람직한 미정 차이가 따라 및 지원 기능, 특히 hello 보안 영역 증가 하는 모든 소프트웨어와 마찬가지로 추가 작업을 제공 합니다.

| 기능 | VM | 컨테이너 |
|:--- | --- | --- |
| “기본” 보안 지원 |tooa 제어력 |tooa 약간 수준과 |
| 디스크에 필요한 메모리 |전체 OS + 앱 |앱 요구 사항만 적용됨 |
| Toostart 하는데 걸리는 시간 |매우 김: OS 부팅 및 앱 로딩 |실질적으로 더 짧은: 앱 커널 이미 실행 되 고 toostart 필요는 전용 |
| 이식성 |적절한 준비로 이식 가능 |이미지 형식으로 이식 가능. 일반적으로 더 작음 |
| 이미지 자동화 |OS와 앱에 따라 크게 다름 |[Docker 레지스트리](https://registry.hub.docker.com/)및 기타 |

## <a name="creating-and-managing-groups-of-vms-and-containers"></a>VM 및 컨테이너 그룹 생성 및 관리
이 시점에서 설계자, 개발자, 또는 IT 운영 전문가라면 "이걸 다 자동화할 수 있다니 진정한 DCaaS(Data-Center-As-A-Service)야!"라고 할지도 모르겠습니다.

맞습니다, 인할 수 있으며 원하는 수 있으며이 중 대다수가 수 이미를 사용, Azure Vm의 그룹을 관리 한 종종 hello로 스크립트를 사용 하 여 사용자 지정 코드를 넣을 수 있는 시스템의 [Windows 용 CustomScriptingExtension](https://msdn.microsoft.com/library/azure/dn781373.aspx) 또는 hello [Linux 용 CustomScriptingExtension](https://azure.microsoft.com/blog/2014/08/20/automate-linux-vm-customization-tasks-using-customscript-extension/)합니다. 이미&mdash;사용하고 있겠지만&mdash;PowerShell 또는 Azure CLI 스크립트를 사용하여 Azure를 배포할 수 있습니다.

이러한 기능은 종종 후 마이그레이션된 tootools 같은 [Puppet](https://puppetlabs.com/) 및 [Chef](https://www.chef.io/) tooautomate hello의 생성 및 대규모 Vm에 대 한 구성 합니다. (다음은 몇 가지 링크 너무[Azure와 함께 이러한 도구를 사용 하 여](#tools-for-working-with-containers).)

### <a name="azure-resource-group-templates"></a>Azure 리소스 그룹 템플릿
Azure의 hello 출시 최근 [Azure 리소스 관리](../articles/resource-manager-deployment-model.md) REST API 및 PowerShell 및 Azure CLI 도구 toouse 업데이트 하기 쉽게 합니다. 배포, 수정 또는 사용 하 여 전체 응용 프로그램 토폴로지를 다시 배포 [Azure 리소스 관리자 템플릿을](../articles/resource-group-authoring-templates.md) hello Azure 리소스 관리 API를 사용 하 여 사용:

* hello [템플릿을 사용 하 여 Azure 포털](https://github.com/Azure/azure-quickstart-templates)&mdash;힌트를 hello "DeployToAzure" 단추를 사용 합니다.
* hello [Azure CLI](../articles/virtual-machines/linux/create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="deployment-and-management-of-entire-groups-of-azure-vms-and-containers"></a>전체 Azure VM 및 컨테이너 그룹의 배포 및 관리
몇몇 인기 시스템에서는 전체 Azure VM 그룹을 배포하고 거기에 Docker 또는 기타 Linux 컨테이너 호스트 시스템을 자동화 가능한 그룹으로 설치할 수 있습니다. 직접 링크 참조 hello [컨테이너 및 도구](#containers-and-vm-technologies) 아래 섹션. 이 목록은 완벽 하지는이 tooa 우선 범위 내에서 수행 하는 여러 시스템을 있습니다. 또한 이 시스템들은 사용자의 기술과 시나리오에 따라 유용할 수도, 유용하지 않을 수도 있습니다.

Docker는 그 자체에 VM 생성 도구([Docker 컴퓨터](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))와 로드 밸런싱 Docker 컨테이너 클러스터 관리 도구([swarm](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json))가 있습니다. 또한 hello [Azure Docker VM 확장](https://github.com/Azure/azure-docker-extension/blob/master/README.md) 에 대 한 기본 지원과 함께 제공 [ `docker-compose` ](https://docs.docker.com/compose/), 여러 컨테이너 간에 응용 프로그램 컨테이너를 구성 하는 배포할 수 있습니다.

[Mesosphere의 DCOS(데이터 센터 운영체제)](http://docs.mesosphere.com)도 사용해 볼만 합니다. DCOS hello 오픈 소스 기반 [mesos](http://mesos.apache.org/) "분산된 시스템 커널" 주소를 지정할 수 하나의 서비스로 데이터 센터 tootreat 있습니다 수 있도록 합니다. DCOS에는 [Spark](http://spark.apache.org/), [Kafka](http://kafka.apache.org/) 등의 여러 중요한 시스템에 기본 제공되는 패키지뿐만 아니라 [Marathon](https://mesosphere.github.io/marathon/)(컨테이너 제어 시스템) 및 [Chronos](https://mesos.github.io/chronos/)(분산형 스케줄러) 같은 기본 제공 서비스가 있습니다. Mesos는 Twitter, AirBnb, 기타 큰 웹 비즈니스의 경험을 바탕으로 탄생했습니다. 사용할 수도 있습니다 **swarm** hello 오케스트레이션 엔진으로 합니다.

[kubernetes](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/) 역시 Google의 경험에 기반하여 탄생한 VM 및 컨테이너 그룹 관리용 공개 소스 시스템입니다. 사용할 수도 있습니다 [와 kubernetes 직물 네트워킹 지원을 나타내는 tooprovide](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)합니다.

[Deis](http://deis.io/overview/) 오픈 소스 "플랫폼-as a Service" (PaaS) 쉽게 toodeploy 수행 하 고 사용자의 서버에서 응용 프로그램 관리 합니다. Deis Docker 및 CoreOS tooprovide Heroku 영감을 얻은 워크플로와 경량 PaaS 빌드합니다.

Linux에서 배포한 [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)는 최적화된 공간을 차지하고 Docker를 지원하며 [rkt](https://github.com/coreos/rkt)라 불리는 자체 컨테이너 시스템을 가지고 있으며 [fleet](https://coreos.com/fleet/docs/latest/)라 불리는 컨테이너 그룹 관리 도구도 제공합니다.

또 다른 인기 Linux 제품인 Ubuntu는 Docker를 매우 적극적으로 지원하며 [Linux(LXC 스타일) 클러스터](https://help.ubuntu.com/lts/serverguide/lxc.html)도 지원합니다.

## <a name="tools-for-working-with-azure-vms-and-containers"></a>Azure VM 및 컨테이너와 호환되는 도구
컨테이너와 Azure VM으로 작업 시 도구가 필요합니다. 이 섹션의 일부 hello 가장 유용 하거나 중요 한 개념 및 컨테이너, 그룹 및 hello 더 큰 구성 하는 방법에 대 한 도구와 함께 사용 하는 오케스트레이션 도구 목록이 표시 됩니다.

> [!NOTE]
> 이 영역은 매우 신속 하 게 변경 하 고이 항목 및 해당 링크를 toodate 우리의 최상의 tookeep 작업이 수행 됩니다, 동안는 잘 것이 불가능 한 키를 누릅니다. 관심 있는 주제 tookeep toodate 검색 하 여 있는지 확인 하십시오!
>
>

### <a name="containers-and-vm-technologies"></a>컨테이너 및 VM 기술
일부 Linux 컨테이너 기술:

* [Docker](https://www.docker.com)
* [LXC](https://linuxcontainers.org/)
* [CoreOS 및 rkt](https://github.com/coreos/rkt)
* [공개 컨테이너 프로젝트](http://opencontainers.org/)
* [RancherOS](http://rancher.com/rancher-os/)

Windows 컨테이너 링크:

* [Windows 컨테이너](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)

Visual Studio Docker 링크:

* [Visual Studio Tools for Docker](https://docs.microsoft.com/en-us/dotnet/core/docker/visual-studio-tools-for-docker)

Docker 도구:

* [Docker 데몬](https://docs.docker.com/installation/#installation)
* Docker 클라이언트
  * [Chocolatey의 Windows Docker 클라이언트](https://chocolatey.org/packages/docker)
  * [Docker 설치 지침](https://docs.docker.com/installation/#installation)

Microsoft Azure의 Docker:

* [Azure의 Linux용 Docker VM 확장](../articles/virtual-machines/linux/dockerextension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure Docker VM 확장 프로그램 사용자 가이드](https://github.com/Azure/azure-docker-extension/blob/master/README.md)
* [Hello Azure CLI (명령줄 인터페이스 Azure)에서 Docker VM 확장 hello를 사용 하 여](../articles/virtual-machines/linux/classic/cli-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Hello Azure 포털에서에서 Docker VM 확장 hello를 사용 하 여](../articles/virtual-machines/linux/classic/portal-use-docker.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [어떻게 toouse docker-Azure에서 컴퓨터](../articles/virtual-machines/linux/docker-machine.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [방법으로 Azure에서 웜 toouse docker](../articles/virtual-machines/virtual-machines-linux-docker-swarm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure 가상 컴퓨터에서 Docker 및 Compose 시작](../articles/virtual-machines/linux/docker-compose-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure에서 Azure 리소스 그룹 템플릿 toocreate Docker 호스트를 신속 하 게 사용](https://github.com/Azure/azure-quickstart-templates/tree/master/docker-simple-on-ubuntu)
* [에 대 한 기본 제공 지원 hello `compose` ](https://github.com/Azure/azure-docker-extension#11-public-configuration-keys) 포함 된 응용 프로그램에 대 한
* [Azure에서 Docker 개인 레지스트리 구현](../articles/virtual-machines/virtual-machines-linux-docker-registry-in-blob-storage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Linux 배포 도구 및 Azure 예시:

* [CoreOS](https://coreos.com/os/docs/latest/booting-on-azure.html)

구성, 클러스터 관리, 컨테이너 오케스트레이션:

* [CoreOS의 Fleet](https://coreos.com/fleet/docs/latest/)
* Deis

  * [CoreOS 및 직물 tooautomated Kubernetes 클러스터 배포 가이드를 완료 합니다.](https://github.com/GoogleCloudPlatform/kubernetes/blob/master/docs/getting-started-guides/coreos/azure/README.md#kubernetes-on-azure-with-coreos-and-weave)
  * [Kubernetes Visualizer](https://azure.microsoft.com/blog/2014/08/28/hackathon-with-kubernetes-on-azure/)
* [Mesos](http://mesos.apache.org/)

  * [Mesosphere의 데이터 센터 운영체제(DCOS)](https://docs.mesosphere.com/1.7/overview/design/azure-container-service/)
* [Jenkins](https://jenkins.io/) 및 [Hudson](http://hudson-ci.org/)

  * [Azure용 Jenkins VM Agent 플러그인](https://wiki.jenkins.io/display/JENKINS/Azure+VM+Agents+plugin)
  * [GitHub 리포지토리: Azure용 Jenkins Storage 플러그인](https://github.com/jenkinsci/windows-azure-storage-plugin)
  * [타사: Azure용 Hudson 슬레이브 플러그인](http://wiki.hudson-ci.org/display/HUDSON/Azure+Slave+Plugin)
  * [타사: Azure용 Hudson Storage 플러그인](https://github.com/hudson3-plugins/windows-azure-storage-plugin)
* [Azure Automation](https://azure.microsoft.com/services/automation/)

  * [비디오: 어떻게 tooUse Linux Vm과 Azure 자동화](http://channel9.msdn.com/Shows/Azure-Friday/Azure-Automation-104-managing-Linux-and-creating-Modules-with-Joe-Levy)
* Linux용 Powershell DSC

  * [블로그: 어떻게 toodo Linux 용 Powershell DSC](http://blogs.technet.com/b/privatecloud/archive/2014/05/19/powershell-dsc-for-linux-step-by-step.aspx)
  * [GitHub: Docker 클라이언트 DSC](https://github.com/anweiss/DockerClientDSC)

## <a name="next-steps"></a>다음 단계
[Docker](https://www.docker.com) 및 [Windows 컨테이너](https://msdn.microsoft.com/virtualization/windowscontainers/about/about_overview)를 확인하세요.

<!--Anchors-->
[microservices]: http://martinfowler.com/articles/microservices.html
[microservice]: http://martinfowler.com/articles/microservices.html
<!--Image references-->
