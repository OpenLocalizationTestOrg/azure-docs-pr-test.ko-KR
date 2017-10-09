# <a name="securing-docker-containers-in-azure-container-service"></a>Azure Container Service에서 Docker 컨테이너 보안

이 문서에서는 Azure Container Service에 배포된 Docker 컨테이너 보호를 위한 고려 사항과 권장 사항을 소개합니다. 이러한 고려 사항 중 많은 적용 일반적으로 tooDocker 컨테이너 Azure 또는 다른 환경에 배포 됩니다. 

## <a name="image-security"></a>이미지 보안

컨테이너는 하나 이상의 리포지토리에 저장된 이미지에서 작성됩니다. 이러한 저장소 toopublic 및 개인 컨테이너 레지스트리에 속할 수 있습니다. 공용 레지스트리의 예는 [Docker 허브](https://hub.docker.com/)입니다. 개인 등록의 예로 hello [Docker Trusted Registry](https://docs.docker.com/datacenter/dtr/2.0/), 온-프레미스 설치 될 수 있습니다 또는 가상 사설 클라우드에서 합니다. [Azure Container Registry](../articles/container-registry/container-registry-intro.md)를 포함한 클라우드 기반 개인 컨테이너 레지스트리 서비스도 있습니다.

### <a name="public-and-private-images"></a>공용 및 개인 이미지
일반적으로, 공개적으로 게시된 소프트웨어 패키지와 마찬가지로 공개적으로 사용 가능한 컨테이너 이미지는 보안을 보장하지 않습니다. 컨테이너 이미지는 여러 소프트웨어 계층으로 구성되며 각 소프트웨어 계층은 취약점이 있을 수 있습니다. Hello 컨테이너 이미지의 키 toounderstand hello 원점, hello 이미지 (또는 경우에 신뢰할 수 있는 소스 하지 toodetermine)의 hello 소유자를 포함 하 여 hello를 구성 하는 소프트웨어 계층 이며 hello 소프트웨어 버전입니다. 

예를 들어, 공식 toohello 이동 [nginx 리포지토리](https://hub.docker.com/_/nginx/) Docker 허브에서 toohello 이동 **태그** 탭을 각 이미지의 색으로 구분 된 취약성을 표시 합니다. 각 색은 hello 이미지의 소프트웨어 계층의 hello 취약점을 보여 줍니다. Docker 허브에서 취약성 검색에 대한 자세한 내용은 [Docker 허브에서 공식적 리포지토리 이해](https://blog.docker.com/2015/06/understanding-official-repos-docker-hub/)를 참조하세요.

![Docker 허브에서 Nginx 이미지](./media/container-service-security/docker-hub-nginx.png)

기업은 처리 깊이 및에 대 한 보안 및 tooprotect 보안 공격 으로부터 자신 해야 저장 Azure 컨테이너 레지스트리 또는 Docker Trusted Registry 같은 개인 레지스트리에서 이미지를 검색 합니다. Azure 컨테이너 레지스트리 지원 추가 tooproviding 관리 되는 개인 레지스트리 [서비스 보안 주체 기반 인증](../articles/container-registry/container-registry-authentication.md) 기본 인증 흐름의 경우에 대 한 역할 기반 액세스를 포함 하 여 Azure Active Directory를 통해 읽기 전용, 쓰기 및 소유자 권한을 합니다.

### <a name="image-security-scanning"></a>이미지 보안 검색

개인 레지스트리를 사용 하는 경우에 추가 보안 유효성 검사에 대 한 솔루션을 검색 하는 것이 좋습니다 toouse 이미지 됩니다. 각 소프트웨어 계층 컨테이너 이미지에는 잠재적으로 발생 하기 쉬운 toovulnerabilities hello 컨테이너 이미지의 다른 레이어 무관 합니다. 점점 더 회사 컨테이너 기술을 기반으로 프로덕션 작업의 배포를 시작, 검색 하는 이미지 중요 tooensure 조직에 대 한 보안 위협 방지 되 됩니다. 

모니터링 및와 같은 솔루션을 검색 하는 보안 [Twistlock](https://www.twistlock.com/2016/11/07/twistlock-supports-azure-container-registry) 및 [바다색 보안](http://blog.aquasec.com/image-vulnerability-scanning-in-azure-container-registry), 맺음 수 사용된 tooscan 개인 레지스트리 ()에 컨테이너 이미지 있고 잠재적인 취약성을 식별 합니다. 제공 것이 중요 toounderstand hello 깊이의 해당 hello 다양 한 솔루션을 검색 합니다. 예를 들어, 일부 솔루션은 알려진 취약성에 대해서만 이미지 계층을 교차 검증할 수 있습니다. 이러한 솔루션에 특정 패키지 관리자 소프트웨어를 통해 빌드할 수 tooverify 이미지 계층의 소프트웨어를 사용할 수 없습니다. 다른 솔루션은 보다 심도 있는 검색 통합 기능을 포함하며 모든 패키지된 소프트웨어에서 취약성을 발견할 수 있습니다.

### <a name="production-deployment-rules-and-audit"></a>프로덕션 배포 규칙 및 감사
응용 프로그램을 프로덕션에 배포 된. 이미지는 프로덕션 환경에서 사용 하는 몇 가지 규칙 tooensure 연결 되어 있는지와 취약점이 없는지를 포함 하는 필수 tooset이 있습니다.

* 일반적으로 취약성도 보조를 사용 하 여 이미지 허용 되지 toorun 프로덕션 환경에서 합니다. 또한 프로덕션에 배포 된 모든 이미지 이상적으로 저장 하도록 개인 레지스트리 액세스 가능한 tooa 선택 되는 몇 합니다. 프로덕션 이미지 작은 tooensure 효과적으로 관리할 수는 중요 한 tookeep hello 수 이기도 합니다.

* 공개적으로 사용할 수 있는 컨테이너 이미지 로부터 소프트웨어의 하드 toopinpoint hello 원점 인 이므로 hello 계층의 hello 원본 소스 tooensure 기술에서 좋습니다 toobuild 이미지입니다. 때 한 취약점 화면 자체 기본 제공된 컨테이너 이미지에 고객 빠른 경로 tooa 해결을 찾을 수 있습니다. 공용 이미지와 고객의 공용 이미지 toofix toofind hello 루트 해야 것 하거나 다른 안전한 이미지 hello 게시자에서 가져와야 합니다.

* 철저 하 게 스캔된 이미지를 프로덕션에 배포 된 hello 응용 프로그램의 hello 수명 toobe toodate 보장 되지 않습니다. 이전에 인식 되지 않았으므로 또는 hello 프로덕션 배포 후에 도입 하는 hello 이미지 계층에 대 한 보안 취약성을 보고 될 수 있습니다. 프로덕션에 배포 된 이미지의 정기적 감사는 잠시 후에 업데이트 되지 않은 되거나 만료 된 필요한 tooidentify 이미지입니다. 하나는 청록색 개발 방법 및 가동 중지 시간 없이 업그레이드 메커니즘 tooupdate 컨테이너 이미지를 롤링 사용할 수 있습니다. 이미지 검색 hello 앞 섹션에서에서 설명 하는 도구와 함께 수행할 수 있습니다. 

* CI (연속 통합) 파이프라인 toobuild 이미지 및 통합된 보안 검사 보안 컨테이너 이미지와 사설 레지스트리 보안 유지 유용할 수 있습니다. hello 취약점 스캔 hello CI 솔루션에 기본 제공 되도록 모든 hello 테스트를 통과 하는 이미지는 배포 된 워크 로드는 프로덕션에서 toohello 개인 레지스트리를 푸시 합니다. CI 파이프라인 오류 취약 이미지 프로덕션 워크 로드 배포에 사용 되는 hello 개인 레지스트리로 밀어넣지 보장 합니다. 또한 이미지 수가 많은 경우에는 이미지 보안 검색을 자동화합니다. 그렇지 않고 이미지에서 보안 취약성을 수동으로 감사하는 것은 매우 번거롭고 오류가 발생하기 쉽습니다.

## <a name="host-level-container-isolation"></a>호스트 수준 컨테이너 격리
고객이 Azure 리소스에 컨테이너 응용 프로그램을 배포하면 리소스 그룹의 구독 수준에서 배포되고 다중 테넌트가 아닙니다. 즉,는 구독을 다른 사용자와 공유 하는 고객을 하는 경우 경계가 없습니다 빌드할 수 있는 hello에 대 한 두 배포 간에 동일한 구독 합니다. 따라서 컨테이너 수준 보안은 보장되지 않습니다. 

컨테이너에서 hello 커널 및 hello 호스트 (이 Azure 컨테이너 서비스의 클러스터에서 Azure VM)의 hello 리소스를 공유 하는 중요 한 toounderstand 이기도 합니다. 따라서 프로덕션에서 실행 중인 컨테이너는 권한 없는 사용자 모드로 실행되어야 합니다. 루트 권한이 있는 컨테이너를 실행 하면 hello 전체 환경을 해칠 수 있습니다. 컨테이너에서 루트 수준 액세스를 통해 해커 액세스할 수 있습니다 hello 호스트에 전체 루트 권한을 toohello 합니다. 또한 읽기 전용 파일 시스템을 사용 하 여 중요 한 toorun 컨테이너는 것입니다. 이렇게 하면 사용자가 액세스 손상 toohello 컨테이너 toowrite 악성 스크립트 toohello 액세스할 tooother 파일 및 파일 시스템 않습니다. 마찬가지로, 것 hello 리소스 (예: 메모리, CPU 및 네트워크 대역폭) 중요 한 toolimit tooa 컨테이너를 할당 합니다. 이 리소스를 많이 사용 하 고 신용 카드 사기 또는 컨테이너의 다른 hello 호스트 또는 클러스터에서 실행 되지 않을 수 있는 bitcoin 마이닝 등의 잘못 된 작업을 추진 해커가 방지할 수 있습니다.

## <a name="orchestrator-considerations"></a>조정자 고려 사항

Azure Container Service에 제공되는 각 조정자는 고유한 보안 고려 사항을 포함합니다. 예를 들어 컨테이너 서비스에서 직접 SSH 액세스 tooorchestrator 노드를 제한 해야 합니다. 대신, 각 orchestrator UI 또는 명령줄 도구를 사용 해야 하면 (예: `kubectl` Kubernetes에 대 한) hello 호스트에 액세스 하지 않고 toomanage hello 컨테이너 환경. 자세한 내용은 참조 [원격 연결 tooa Kubernetes, DC/OS 또는 docker는 Docker Swarm 클러스터 확인](../articles/container-service/kubernetes/container-service-connect.md)합니다.

Orchestrator에 특정 한 추가 보안 정보에 대 한 hello 다음 리소스를 참조:

* **Kubernetes**: [Kubernetes 배포에 대한 보안 모범 사례](http://blog.kubernetes.io/2016/08/security-best-practices-kubernetes-deployment.html)

* **DC/OS**: [클러스터 보안 설정](https://dcos.io/docs/1.8/administration/securing-your-cluster/)

* **Docker Swarm**: [Docker 보안](https://www.docker.com/docker-security)

## <a name="next-steps"></a>다음 단계

* Docker 아키텍처 및 컨테이너 보안에 대 한 자세한 내용은 [소개 tooContainer 보안](https://www.docker.com/sites/default/files/WP_IntrotoContainerSecurity_08.19.2016.pdf)합니다.

* Azure 플랫폼 보안에 대 한 정보를 참조 hello [Azure 보안 센터](https://www.microsoft.com/en-us/trustcenter/cloudservices/azure)합니다.
