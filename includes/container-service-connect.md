# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a>원격 연결 tooa Kubernetes, DC/OS 또는 docker는 Docker Swarm 클러스터를 확인 합니다.
Azure 컨테이너 서비스 클러스터를 만든 다음 tooconnect toohello 클러스터 toodeploy 필요와 워크 로드를 관리 합니다. 이 문서에서는 원격 컴퓨터에서 tooconnect toohello 마스터의 hello VM 클러스터 되는 방법을 설명 합니다. 

hello Kubernetes, DC/OS 및 docker는 Docker Swarm 클러스터 로컬 HTTP 끝점을 제공합니다. Kubernetes에 대 한이 끝점에 노출 안전 하 게 되 인터넷 hello, 그리고 hello를 실행 하 여 액세스할 수 `kubectl` 인터넷에 연결 된 모든 컴퓨터에서 명령줄 도구입니다. 

DC/OS 및 docker는 Docker Swarm을 로컬 컴퓨터 toohello 클러스터 관리 시스템에서 보안 셸 SSH 터널을 만들어야 하는 것이 좋습니다. Hello 터널 설정 되 면 hello HTTP 끝점 및 보기 hello orchestrator 웹 인터페이스 (있는 경우) 로컬 시스템에서 사용 하는 명령을 실행할 수 있습니다. 

## <a name="prerequisites"></a>필수 조건

* [Azure Container Service에 배포된](../articles/container-service/dcos-swarm/container-service-deployment.md) Kubernetes, DC/OS 또는 Docker Swarm 클러스터.
* SSH RSA 개인 키 파일을 배포 하는 동안 toohello 공개 키 추가 toohello 클러스터에 해당 합니다. 이러한 명령은 해당 hello 개인 SSH 키가 있는 가정 `$HOME/.ssh/id_rsa` 컴퓨터에 있습니다. 자세한 내용은 [macOS 및 Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) 또는 [Windows](../articles/virtual-machines/linux/ssh-from-windows.md)에 대한 다음 지침을 참조하세요. SSH 연결 hello 작동 하지 않는 경우 해야 너무 [SSH 키를 다시 설정](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)합니다.

## <a name="connect-tooa-kubernetes-cluster"></a>Tooa Kubernetes 클러스터에 연결

이러한 단계 tooinstall 따르고 구성 `kubectl` 컴퓨터에 있습니다.

> [!NOTE] 
> Linux 또는 macOS toorun hello 명령을 사용 하 여이 섹션에서 필요할 `sudo`합니다.
> 

### <a name="install-kubectl"></a>kubectl 설치
한 가지 방법은 tooinstall이이 도구는 toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 명령입니다. 이 명령에 있는지 확인 하는 toorun 있습니다 [설치](/cli/azure/install-az-cli2) 최신 Azure CLI 2.0 hello 및 tooan Azure 계정에에서 기록 (`az login`).

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

최신 hello를 다운로드할 수는 또한 `kubectl` 클라이언트 hello에서 직접 [Kubernetes 해제 페이지](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md)합니다. 자세한 내용은 [kubectl 설치 및 설정](https://kubernetes.io/docs/tasks/kubectl/install/)을 참조하세요.

### <a name="download-cluster-credentials"></a>클러스터 자격 증명 다운로드
설정한 후 `kubectl` toocopy hello 클러스터 자격 증명 tooyour 컴퓨터 필요한 설치 합니다. 한 가지 방법은 toodo get hello 자격 증명은 hello로 `az acs kubernetes get-credentials` 명령입니다. Hello 리소스 그룹의 hello 이름과 hello 컨테이너 서비스 리소스의 hello 이름을 전달 합니다.

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

이 명령은 hello 클러스터 자격 증명을 너무 다운로드`$HOME/.kube/config`여기서 `kubectl` 있는 toobe가 예상 합니다.

사용할 수 있습니다 `scp` toosecurely hello 파일에서 복사 `$HOME/.kube/config` hello 마스터 VM tooyour 로컬 컴퓨터에 있습니다. 예:

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

Windows의 경우 Windows, hello PuTTy 보안 파일 복사 클라이언트 또는 유사한 도구에는 ubuntu Bash를 사용할 수 있습니다.

### <a name="use-kubectl"></a>kubectl 사용

설정한 후 `kubectl` 클러스터의 hello 노드를 나열 하 여 hello 연결을 테스트 구성:

```bash
kubectl get nodes
```

다른 `kubectl` 명령을 사용할 수 있습니다. 예를 들어 hello Kubernetes 대시보드를 볼 수 있습니다. 첫째, 프록시 toohello Kubernetes API 서버를 실행 합니다.

```bash
kubectl proxy
```

hello Kubernetes UI는 이제 //go.microsoft.com/fwlink/: `http://localhost:8001/ui`합니다.

자세한 내용은 참조 hello [Kubernetes 퀵 스타트](http://kubernetes.io/docs/user-guide/quick-start/)합니다.

## <a name="connect-tooa-dcos-or-swarm-cluster"></a>Tooa DC/OS 또는 웜 클러스터에 연결

toouse hello DC/OS 및 Azure 컨테이너 서비스에서 배포 하는 docker는 Docker Swarm 클러스터 로컬 Windows, Linux 또는 macOS 등 시스템에서 이러한 지침 toocreate SSH 터널을 따릅니다. 

> [!NOTE]
> 이러한 지침은 SSH를 통한 TCP 트래픽 터널링에 중점을 둡니다. Hello 내부 클러스터 관리 시스템 중 하나가 지정 된 대화형 SSH 세션을 시작할 수도 있지만이 권장 됩니다. 내부 시스템에 직접 작업할 경우 실수로 구성을 변경할 위험이 있습니다.  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a>Linux 또는 macOS에서 SSH 터널 만들기
Linux 또는 macOS SSH 터널을 만들 때 수행 하는 먼저 hello hello 부하 분산 된 마스터 toolocate hello 공용 DNS 이름입니다. 다음 단계를 수행하세요.


1. Hello에 [Azure 포털](https://portal.azure.com), 컨테이너 서비스 클러스터를 포함 하는 toohello 리소스 그룹을 검색 합니다. 각 리소스 표시 되도록 hello 리소스 그룹을 확장 합니다. 

2. Hello 클릭 **컨테이너 서비스** 리소스 및 클릭 **개요**합니다. hello **마스터 FQDN** hello 클러스터에서 나타나는 **Essentials**합니다. 이 이름은 나중에 사용되므로 저장합니다. 

    ![공용 DNS 이름](./media/container-service-connect/pubdns.png)

    또는 실행 하는 hello `az acs show` 컨테이너 서비스에서 명령을 합니다. Hello에 대 한 확인 **마스터 프로필: fqdn** hello 명령 출력에는 속성입니다.

3. 이제는 셸을 열고 실행 hello `ssh` hello 다음 값을 지정 하 여 명령을: 

    **LOCAL_PORT** 를 hello 터널 tooconnect의 hello 서비스 측에 hello TCP 포트입니다. 웜,이 too2375를 설정 합니다. DC/OS 용이 too80를 설정 합니다. 
    **REMOTE_PORT** tooexpose hello 끝점의 hello 포트입니다. Swarm의 경우 2375 포트를 사용합니다. DC/OS의 경우 포트 80을 사용합니다.  
    **사용자 이름** hello 클러스터를 배포할 때 제공 된 hello 사용자 이름입니다.  
    **DNSPREFIX** hello 클러스터를 배포할 때 제공 하는 hello DNS 접두사입니다.  
    **지역** 리소스 그룹의 위치를 가리키는 hello 영역입니다.  
    **PATH_TO_PRIVATE_KEY** [옵션] hello 경로 toohello 개인 키 hello 클러스터를 만들 때 제공한 toohello 공개 키에 해당 하는입니다. 이 옵션을 사용 하 여 hello로 `-i` 플래그입니다.

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > SSH 연결 포트 hello 2200 이며 표준 포트 22를 hello 하지 않습니다. 둘 이상의 마스터 VM과 클러스터 hello 연결 포트 toohello 첫 번째 마스터 VM입니다.
  > 

  hello 명령은 출력 하지 않고 반환합니다.

Hello 다음 섹션에서에서 DC/OS 및 웜 hello 예제를 참조 합니다.    

### <a name="dcos-tunnel"></a>DC/OS 터널
DC/OS 끝점에 대 한 터널 tooopen hello 다음과 같은 명령을 실행 합니다.

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> 포트 80에 바인딩하는 다른 로컬 프로세스가 없는지 확인합니다. 필요한 경우 포트 80이 아닌 다른 로컬 포트(예: 포트 8080)를 지정할 수 있습니다. 그러나 이 포트를 사용할 경우 일부 웹 UI 링크가 작동하지 않을 수 있습니다.
>

이제 hello 다음 (로컬 포트 80 가정) Url을 통해 로컬 시스템에서 hello DC/OS 끝점에 액세스할 수 있습니다.

* DC/OS: `http://localhost:80/`
* Marathon: `http://localhost:80/marathon`
* Mesos: `http://localhost:80/mesos`

마찬가지로,이 터널을 통해 각 응용 프로그램에 대 한 hello rest Api에 연결할 수 있습니다.

### <a name="swarm-tunnel"></a>Swarm 터널
tooopen 터널 toohello 웜 끝점 hello 다음과 같은 명령을 실행 하는 중:

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> 포트 2375에 바인딩하는 다른 로컬 프로세스가 없는지 확인합니다. 예를 들어 hello Docker 디먼을 로컬로 실행 하는 경우 기본 toouse 포트 2375에서 설정 됩니다. 필요한 경우 포트 2375가 아닌 다른 로컬 포트를 지정할 수 있습니다.
>

이제 hello docker는 Docker Swarm 클러스터 hello Docker 명령줄 인터페이스 (Docker CLI)를 사용 하 여 로컬 시스템에 액세스할 수 있습니다. 설치 지침은 [Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.

DOCKER_HOST 환경 변수 toohello hello 터널에 대해 구성 하는 로컬 포트를 설정 합니다. 

```bash
export DOCKER_HOST=:2375
```

Docker 명령을 해당 터널 toohello docker는 Docker Swarm 클러스터를 실행 합니다. 예:

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a>Windows에서 SSH 터널 만들기
Windows에서 SSH 터널을 만드는 방법은 여러 가지가 있습니다. Ubuntu Bash 실행 하는 Windows 또는 유사한 도구를 경우 macOS 및 Linux에 대 한이 문서의 앞부분에 표시 된 hello SSH 터널링 지침을 따를 수 있습니다. 이 섹션에서는 Windows에서 사용 되는 대신, 다음을 설명 합니다. 어떻게 toouse PuTTY toocreate hello 터널 합니다.

1. [PuTTY 다운로드](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows 시스템입니다.

2. Hello 응용 프로그램을 실행 합니다.

3. Hello 클러스터 관리자 사용자 이름 및 hello hello hello 클러스터의 첫 번째 마스터의 공용 DNS 이름으로 구성 된 호스트 이름을 입력 합니다. hello **호스트 이름** 너무 에서도 비슷하게 보임`azureuser@PublicDNSName`합니다. 2200 hello에 대 한 입력 **포트**합니다.

    ![PuTTY 구성 1](./media/container-service-connect/putty1.png)

4. **SSH > 인증**을 선택합니다. 경로 tooyour 개인 키 파일 (형식.ppk) 인증을 추가 합니다. 와 같은 도구를 사용할 수 [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) 에서 파일을이 toogenerate hello SSH 키 사용 되는 toocreate hello 클러스터입니다.

    ![PuTTY 구성 2](./media/container-service-connect/putty2.png)

5. 선택 **SSH > 터널** 고 포트를 전달 하는 hello 다음 구성:

    * **원본 포트:** DC/OS의 경우 80 또는 Swarm의 경우 2375를 사용합니다.
    * **대상:** localhost:80(DC/OS) 또는 localhost:2375(Swarm)를 사용합니다.

    다음 예제는 hello DC/OS 용 구성 되어 있지만 docker는 Docker Swarm을 다음과 같이 표시 됩니다.

    > [!NOTE]
    > 이 터널을 만들 때 포트 80은 사용 중이 아니어야 합니다.
    > 

    ![PuTTY 구성 3](./media/container-service-connect/putty3.png)

6. 완료 되 면 클릭 **세션 > 저장** toosave hello 연결 구성 합니다.

7. tooconnect toohello PuTTY 세션, 클릭 **열려**합니다. 에 연결할 때 hello PuTTY 이벤트 로그의 hello 포트 구성을 확인할 수 있습니다.

    ![PuTTY 이벤트 로그](./media/container-service-connect/putty4.png)

DC/OS 용 hello 터널을 구성한 후에 액세스할 수 있습니다 hello에서 끝점 관련:

* DC/OS: `http://localhost/`
* Marathon: `http://localhost/marathon`
* Mesos: `http://localhost/mesos`

Docker는 Docker Swarm에 대 한 hello 터널을 구성한 후 Windows 설정을 tooconfigure 라는 시스템 환경 변수를 열고 `DOCKER_HOST` 값 `:2375`합니다. 그런 다음 hello 웜 클러스터 hello Docker CLI를 통해 액세스할 수 있습니다.

## <a name="next-steps"></a>다음 단계
클러스터에서 컨테이너를 배포하고 관리합니다.

* [Azure Container Service 및 Kubernetes로 작업](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [Azure 컨테이너 서비스 및 DC/OS로 작업](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [Azure 컨테이너 서비스 hello 및 docker는 Docker Swarm 작업](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

