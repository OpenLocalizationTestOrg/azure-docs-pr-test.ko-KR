# <a name="make-a-remote-connection-tooa-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="95aa0-101">원격 연결 tooa Kubernetes, DC/OS 또는 docker는 Docker Swarm 클러스터를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-101">Make a remote connection tooa Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="95aa0-102">Azure 컨테이너 서비스 클러스터를 만든 다음 tooconnect toohello 클러스터 toodeploy 필요와 워크 로드를 관리 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-102">After creating an Azure Container Service cluster, you need tooconnect toohello cluster toodeploy and manage workloads.</span></span> <span data-ttu-id="95aa0-103">이 문서에서는 원격 컴퓨터에서 tooconnect toohello 마스터의 hello VM 클러스터 되는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-103">This article describes how tooconnect toohello master VM of hello cluster from a remote computer.</span></span> 

<span data-ttu-id="95aa0-104">hello Kubernetes, DC/OS 및 docker는 Docker Swarm 클러스터 로컬 HTTP 끝점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-104">hello Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="95aa0-105">Kubernetes에 대 한이 끝점에 노출 안전 하 게 되 인터넷 hello, 그리고 hello를 실행 하 여 액세스할 수 `kubectl` 인터넷에 연결 된 모든 컴퓨터에서 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-105">For Kubernetes, this endpoint is securely exposed on hello internet, and you can access it by running hello `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="95aa0-106">DC/OS 및 docker는 Docker Swarm을 로컬 컴퓨터 toohello 클러스터 관리 시스템에서 보안 셸 SSH 터널을 만들어야 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer toohello cluster management system.</span></span> <span data-ttu-id="95aa0-107">Hello 터널 설정 되 면 hello HTTP 끝점 및 보기 hello orchestrator 웹 인터페이스 (있는 경우) 로컬 시스템에서 사용 하는 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-107">After hello tunnel is established, you can run commands which use hello HTTP endpoints and view hello orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="95aa0-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="95aa0-108">Prerequisites</span></span>

* <span data-ttu-id="95aa0-109">[Azure Container Service에 배포된](../articles/container-service/dcos-swarm/container-service-deployment.md) Kubernetes, DC/OS 또는 Docker Swarm 클러스터.</span><span class="sxs-lookup"><span data-stu-id="95aa0-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="95aa0-110">SSH RSA 개인 키 파일을 배포 하는 동안 toohello 공개 키 추가 toohello 클러스터에 해당 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-110">SSH RSA private key file, corresponding toohello public key added toohello cluster during deployment.</span></span> <span data-ttu-id="95aa0-111">이러한 명령은 해당 hello 개인 SSH 키가 있는 가정 `$HOME/.ssh/id_rsa` 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-111">These commands assume that hello private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="95aa0-112">자세한 내용은 [macOS 및 Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) 또는 [Windows](../articles/virtual-machines/linux/ssh-from-windows.md)에 대한 다음 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95aa0-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="95aa0-113">SSH 연결 hello 작동 하지 않는 경우 해야 너무 [SSH 키를 다시 설정](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-113">If hello SSH connection isn't working, you may need too [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-tooa-kubernetes-cluster"></a><span data-ttu-id="95aa0-114">Tooa Kubernetes 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="95aa0-114">Connect tooa Kubernetes cluster</span></span>

<span data-ttu-id="95aa0-115">이러한 단계 tooinstall 따르고 구성 `kubectl` 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-115">Follow these steps tooinstall and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="95aa0-116">Linux 또는 macOS toorun hello 명령을 사용 하 여이 섹션에서 필요할 `sudo`합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-116">On Linux or macOS, you might need toorun hello commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="95aa0-117">kubectl 설치</span><span class="sxs-lookup"><span data-stu-id="95aa0-117">Install kubectl</span></span>
<span data-ttu-id="95aa0-118">한 가지 방법은 tooinstall이이 도구는 toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-118">One way tooinstall this tool is toouse hello `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="95aa0-119">이 명령에 있는지 확인 하는 toorun 있습니다 [설치](/cli/azure/install-az-cli2) 최신 Azure CLI 2.0 hello 및 tooan Azure 계정에에서 기록 (`az login`).</span><span class="sxs-lookup"><span data-stu-id="95aa0-119">toorun this command, make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="95aa0-120">최신 hello를 다운로드할 수는 또한 `kubectl` 클라이언트 hello에서 직접 [Kubernetes 해제 페이지](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-120">Alternatively, you can download hello latest `kubectl` client directly from hello [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="95aa0-121">자세한 내용은 [kubectl 설치 및 설정](https://kubernetes.io/docs/tasks/kubectl/install/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95aa0-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="95aa0-122">클러스터 자격 증명 다운로드</span><span class="sxs-lookup"><span data-stu-id="95aa0-122">Download cluster credentials</span></span>
<span data-ttu-id="95aa0-123">설정한 후 `kubectl` toocopy hello 클러스터 자격 증명 tooyour 컴퓨터 필요한 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-123">Once you have `kubectl` installed, you need toocopy hello cluster credentials tooyour machine.</span></span> <span data-ttu-id="95aa0-124">한 가지 방법은 toodo get hello 자격 증명은 hello로 `az acs kubernetes get-credentials` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-124">One way toodo get hello credentials is with hello `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="95aa0-125">Hello 리소스 그룹의 hello 이름과 hello 컨테이너 서비스 리소스의 hello 이름을 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-125">Pass hello name of hello resource group and hello name of hello container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="95aa0-126">이 명령은 hello 클러스터 자격 증명을 너무 다운로드`$HOME/.kube/config`여기서 `kubectl` 있는 toobe가 예상 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-126">This command downloads hello cluster credentials too`$HOME/.kube/config`, where `kubectl` expects it toobe located.</span></span>

<span data-ttu-id="95aa0-127">사용할 수 있습니다 `scp` toosecurely hello 파일에서 복사 `$HOME/.kube/config` hello 마스터 VM tooyour 로컬 컴퓨터에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-127">Alternatively, you can use `scp` toosecurely copy hello file from `$HOME/.kube/config` on hello master VM tooyour local machine.</span></span> <span data-ttu-id="95aa0-128">예:</span><span class="sxs-lookup"><span data-stu-id="95aa0-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="95aa0-129">Windows의 경우 Windows, hello PuTTy 보안 파일 복사 클라이언트 또는 유사한 도구에는 ubuntu Bash를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-129">If you are on Windows, you can use Bash on Ubuntu on Windows, hello PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="95aa0-130">kubectl 사용</span><span class="sxs-lookup"><span data-stu-id="95aa0-130">Use kubectl</span></span>

<span data-ttu-id="95aa0-131">설정한 후 `kubectl` 클러스터의 hello 노드를 나열 하 여 hello 연결을 테스트 구성:</span><span class="sxs-lookup"><span data-stu-id="95aa0-131">Once you have `kubectl` configured, test hello connection by listing hello nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="95aa0-132">다른 `kubectl` 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="95aa0-133">예를 들어 hello Kubernetes 대시보드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-133">For example, you can view hello Kubernetes Dashboard.</span></span> <span data-ttu-id="95aa0-134">첫째, 프록시 toohello Kubernetes API 서버를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-134">First, run a proxy toohello Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="95aa0-135">hello Kubernetes UI는 이제 //go.microsoft.com/fwlink/: `http://localhost:8001/ui`합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-135">hello Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="95aa0-136">자세한 내용은 참조 hello [Kubernetes 퀵 스타트](http://kubernetes.io/docs/user-guide/quick-start/)합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-136">For more information, see hello [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-tooa-dcos-or-swarm-cluster"></a><span data-ttu-id="95aa0-137">Tooa DC/OS 또는 웜 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="95aa0-137">Connect tooa DC/OS or Swarm cluster</span></span>

<span data-ttu-id="95aa0-138">toouse hello DC/OS 및 Azure 컨테이너 서비스에서 배포 하는 docker는 Docker Swarm 클러스터 로컬 Windows, Linux 또는 macOS 등 시스템에서 이러한 지침 toocreate SSH 터널을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-138">toouse hello DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions toocreate a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="95aa0-139">이러한 지침은 SSH를 통한 TCP 트래픽 터널링에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="95aa0-140">Hello 내부 클러스터 관리 시스템 중 하나가 지정 된 대화형 SSH 세션을 시작할 수도 있지만이 권장 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-140">You can also start an interactive SSH session with one of hello internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="95aa0-141">내부 시스템에 직접 작업할 경우 실수로 구성을 변경할 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="95aa0-142">Linux 또는 macOS에서 SSH 터널 만들기</span><span class="sxs-lookup"><span data-stu-id="95aa0-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="95aa0-143">Linux 또는 macOS SSH 터널을 만들 때 수행 하는 먼저 hello hello 부하 분산 된 마스터 toolocate hello 공용 DNS 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-143">hello first thing that you do when you create an SSH tunnel on Linux or macOS is toolocate hello public DNS name of hello load-balanced masters.</span></span> <span data-ttu-id="95aa0-144">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="95aa0-144">Follow these steps:</span></span>


1. <span data-ttu-id="95aa0-145">Hello에 [Azure 포털](https://portal.azure.com), 컨테이너 서비스 클러스터를 포함 하는 toohello 리소스 그룹을 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-145">In hello [Azure portal](https://portal.azure.com), browse toohello resource group containing your container service cluster.</span></span> <span data-ttu-id="95aa0-146">각 리소스 표시 되도록 hello 리소스 그룹을 확장 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-146">Expand hello resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="95aa0-147">Hello 클릭 **컨테이너 서비스** 리소스 및 클릭 **개요**합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-147">Click hello **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="95aa0-148">hello **마스터 FQDN** hello 클러스터에서 나타나는 **Essentials**합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-148">hello **Master FQDN** of hello cluster appears under **Essentials**.</span></span> <span data-ttu-id="95aa0-149">이 이름은 나중에 사용되므로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-149">Save this name for later use.</span></span> 

    ![공용 DNS 이름](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="95aa0-151">또는 실행 하는 hello `az acs show` 컨테이너 서비스에서 명령을 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-151">Alternatively, run hello `az acs show` command on your container service.</span></span> <span data-ttu-id="95aa0-152">Hello에 대 한 확인 **마스터 프로필: fqdn** hello 명령 출력에는 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-152">Look for hello **Master Profile:fqdn** property in hello command output.</span></span>

3. <span data-ttu-id="95aa0-153">이제는 셸을 열고 실행 hello `ssh` hello 다음 값을 지정 하 여 명령을:</span><span class="sxs-lookup"><span data-stu-id="95aa0-153">Now open a shell and run hello `ssh` command by specifying hello following values:</span></span> 

    <span data-ttu-id="95aa0-154">**LOCAL_PORT** 를 hello 터널 tooconnect의 hello 서비스 측에 hello TCP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-154">**LOCAL_PORT** is hello TCP port on hello service side of hello tunnel tooconnect to.</span></span> <span data-ttu-id="95aa0-155">웜,이 too2375를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-155">For Swarm, set this too2375.</span></span> <span data-ttu-id="95aa0-156">DC/OS 용이 too80를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-156">For DC/OS, set this too80.</span></span> 
    <span data-ttu-id="95aa0-157">**REMOTE_PORT** tooexpose hello 끝점의 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-157">**REMOTE_PORT** is hello port of hello endpoint that you want tooexpose.</span></span> <span data-ttu-id="95aa0-158">Swarm의 경우 2375 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="95aa0-159">DC/OS의 경우 포트 80을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="95aa0-160">**사용자 이름** hello 클러스터를 배포할 때 제공 된 hello 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-160">**USERNAME** is hello user name that was provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="95aa0-161">**DNSPREFIX** hello 클러스터를 배포할 때 제공 하는 hello DNS 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-161">**DNSPREFIX** is hello DNS prefix that you provided when you deployed hello cluster.</span></span>  
    <span data-ttu-id="95aa0-162">**지역** 리소스 그룹의 위치를 가리키는 hello 영역입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-162">**REGION** is hello region in which your resource group is located.</span></span>  
    <span data-ttu-id="95aa0-163">**PATH_TO_PRIVATE_KEY** [옵션] hello 경로 toohello 개인 키 hello 클러스터를 만들 때 제공한 toohello 공개 키에 해당 하는입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is hello path toohello private key that corresponds toohello public key you provided when you created hello cluster.</span></span> <span data-ttu-id="95aa0-164">이 옵션을 사용 하 여 hello로 `-i` 플래그입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-164">Use this option with hello `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="95aa0-165">SSH 연결 포트 hello 2200 이며 표준 포트 22를 hello 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-165">hello SSH connection port is 2200 and not hello standard port 22.</span></span> <span data-ttu-id="95aa0-166">둘 이상의 마스터 VM과 클러스터 hello 연결 포트 toohello 첫 번째 마스터 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-166">In a cluster with more than one master VM, this is hello connection port toohello first master VM.</span></span>
  > 

  <span data-ttu-id="95aa0-167">hello 명령은 출력 하지 않고 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-167">hello command returns without output.</span></span>

<span data-ttu-id="95aa0-168">Hello 다음 섹션에서에서 DC/OS 및 웜 hello 예제를 참조 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-168">See hello examples for DC/OS and Swarm in hello following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="95aa0-169">DC/OS 터널</span><span class="sxs-lookup"><span data-stu-id="95aa0-169">DC/OS tunnel</span></span>
<span data-ttu-id="95aa0-170">DC/OS 끝점에 대 한 터널 tooopen hello 다음과 같은 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-170">tooopen a tunnel for DC/OS endpoints, run a command like hello following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="95aa0-171">포트 80에 바인딩하는 다른 로컬 프로세스가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="95aa0-172">필요한 경우 포트 80이 아닌 다른 로컬 포트(예: 포트 8080)를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="95aa0-173">그러나 이 포트를 사용할 경우 일부 웹 UI 링크가 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="95aa0-174">이제 hello 다음 (로컬 포트 80 가정) Url을 통해 로컬 시스템에서 hello DC/OS 끝점에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-174">You can now access hello DC/OS endpoints from your local system through hello following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="95aa0-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="95aa0-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="95aa0-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="95aa0-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="95aa0-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="95aa0-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="95aa0-178">마찬가지로,이 터널을 통해 각 응용 프로그램에 대 한 hello rest Api에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-178">Similarly, you can reach hello rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="95aa0-179">Swarm 터널</span><span class="sxs-lookup"><span data-stu-id="95aa0-179">Swarm tunnel</span></span>
<span data-ttu-id="95aa0-180">tooopen 터널 toohello 웜 끝점 hello 다음과 같은 명령을 실행 하는 중:</span><span class="sxs-lookup"><span data-stu-id="95aa0-180">tooopen a tunnel toohello Swarm endpoint, run a command like hello following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="95aa0-181">포트 2375에 바인딩하는 다른 로컬 프로세스가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="95aa0-182">예를 들어 hello Docker 디먼을 로컬로 실행 하는 경우 기본 toouse 포트 2375에서 설정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-182">For example, if you are running hello Docker daemon locally, it's set by default toouse port 2375.</span></span> <span data-ttu-id="95aa0-183">필요한 경우 포트 2375가 아닌 다른 로컬 포트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="95aa0-184">이제 hello docker는 Docker Swarm 클러스터 hello Docker 명령줄 인터페이스 (Docker CLI)를 사용 하 여 로컬 시스템에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-184">Now you can access hello Docker Swarm cluster using hello Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="95aa0-185">설치 지침은 [Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="95aa0-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="95aa0-186">DOCKER_HOST 환경 변수 toohello hello 터널에 대해 구성 하는 로컬 포트를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-186">Set your DOCKER_HOST environment variable toohello local port you configured for hello tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="95aa0-187">Docker 명령을 해당 터널 toohello docker는 Docker Swarm 클러스터를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-187">Run Docker commands that tunnel toohello Docker Swarm cluster.</span></span> <span data-ttu-id="95aa0-188">예:</span><span class="sxs-lookup"><span data-stu-id="95aa0-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="95aa0-189">Windows에서 SSH 터널 만들기</span><span class="sxs-lookup"><span data-stu-id="95aa0-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="95aa0-190">Windows에서 SSH 터널을 만드는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="95aa0-191">Ubuntu Bash 실행 하는 Windows 또는 유사한 도구를 경우 macOS 및 Linux에 대 한이 문서의 앞부분에 표시 된 hello SSH 터널링 지침을 따를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow hello SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="95aa0-192">이 섹션에서는 Windows에서 사용 되는 대신, 다음을 설명 합니다. 어떻게 toouse PuTTY toocreate hello 터널 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-192">As an alternative on Windows, this section describes how toouse PuTTY toocreate hello tunnel.</span></span>

1. <span data-ttu-id="95aa0-193">[PuTTY 다운로드](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) tooyour Windows system.</span></span>

2. <span data-ttu-id="95aa0-194">Hello 응용 프로그램을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-194">Run hello application.</span></span>

3. <span data-ttu-id="95aa0-195">Hello 클러스터 관리자 사용자 이름 및 hello hello hello 클러스터의 첫 번째 마스터의 공용 DNS 이름으로 구성 된 호스트 이름을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-195">Enter a host name that is comprised of hello cluster admin user name and hello public DNS name of hello first master in hello cluster.</span></span> <span data-ttu-id="95aa0-196">hello **호스트 이름** 너무 에서도 비슷하게 보임`azureuser@PublicDNSName`합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-196">hello **Host Name** looks similar too`azureuser@PublicDNSName`.</span></span> <span data-ttu-id="95aa0-197">2200 hello에 대 한 입력 **포트**합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-197">Enter 2200 for hello **Port**.</span></span>

    ![PuTTY 구성 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="95aa0-199">**SSH > 인증**을 선택합니다. 경로 tooyour 개인 키 파일 (형식.ppk) 인증을 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-199">Select **SSH > Auth**. Add a path tooyour private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="95aa0-200">와 같은 도구를 사용할 수 [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) 에서 파일을이 toogenerate hello SSH 키 사용 되는 toocreate hello 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-200">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) toogenerate this file from hello SSH key used toocreate hello cluster.</span></span>

    ![PuTTY 구성 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="95aa0-202">선택 **SSH > 터널** 고 포트를 전달 하는 hello 다음 구성:</span><span class="sxs-lookup"><span data-stu-id="95aa0-202">Select **SSH > Tunnels** and configure hello following forwarded ports:</span></span>

    * <span data-ttu-id="95aa0-203">**원본 포트:** DC/OS의 경우 80 또는 Swarm의 경우 2375를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-203">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="95aa0-204">**대상:** localhost:80(DC/OS) 또는 localhost:2375(Swarm)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-204">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="95aa0-205">다음 예제는 hello DC/OS 용 구성 되어 있지만 docker는 Docker Swarm을 다음과 같이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-205">hello following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="95aa0-206">이 터널을 만들 때 포트 80은 사용 중이 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-206">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![PuTTY 구성 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="95aa0-208">완료 되 면 클릭 **세션 > 저장** toosave hello 연결 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-208">When you're finished, click **Session > Save** toosave hello connection configuration.</span></span>

7. <span data-ttu-id="95aa0-209">tooconnect toohello PuTTY 세션, 클릭 **열려**합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-209">tooconnect toohello PuTTY session, click **Open**.</span></span> <span data-ttu-id="95aa0-210">에 연결할 때 hello PuTTY 이벤트 로그의 hello 포트 구성을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-210">When you connect, you can see hello port configuration in hello PuTTY event log.</span></span>

    ![PuTTY 이벤트 로그](./media/container-service-connect/putty4.png)

<span data-ttu-id="95aa0-212">DC/OS 용 hello 터널을 구성한 후에 액세스할 수 있습니다 hello에서 끝점 관련:</span><span class="sxs-lookup"><span data-stu-id="95aa0-212">After you've configured hello tunnel for DC/OS, you can access hello related endpoints at:</span></span>

* <span data-ttu-id="95aa0-213">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="95aa0-213">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="95aa0-214">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="95aa0-214">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="95aa0-215">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="95aa0-215">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="95aa0-216">Docker는 Docker Swarm에 대 한 hello 터널을 구성한 후 Windows 설정을 tooconfigure 라는 시스템 환경 변수를 열고 `DOCKER_HOST` 값 `:2375`합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-216">After you've configured hello tunnel for Docker Swarm, open your Windows settings tooconfigure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="95aa0-217">그런 다음 hello 웜 클러스터 hello Docker CLI를 통해 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-217">Then, you can access hello Swarm cluster through hello Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95aa0-218">다음 단계</span><span class="sxs-lookup"><span data-stu-id="95aa0-218">Next steps</span></span>
<span data-ttu-id="95aa0-219">클러스터에서 컨테이너를 배포하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="95aa0-219">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="95aa0-220">Azure Container Service 및 Kubernetes로 작업</span><span class="sxs-lookup"><span data-stu-id="95aa0-220">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="95aa0-221">Azure 컨테이너 서비스 및 DC/OS로 작업</span><span class="sxs-lookup"><span data-stu-id="95aa0-221">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="95aa0-222">Azure 컨테이너 서비스 hello 및 docker는 Docker Swarm 작업</span><span class="sxs-lookup"><span data-stu-id="95aa0-222">Work with hello Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

