# <a name="make-a-remote-connection-to-a-kubernetes-dcos-or-docker-swarm-cluster"></a><span data-ttu-id="d5d3b-101">Kubernetes, DC/OS 또는 Docker Swarm 클러스터에 원격 연결</span><span class="sxs-lookup"><span data-stu-id="d5d3b-101">Make a remote connection to a Kubernetes, DC/OS, or Docker Swarm cluster</span></span>
<span data-ttu-id="d5d3b-102">Azure Container Service 클러스터를 만든 후에 클러스터에 연결하여 워크로드를 배포하고 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-102">After creating an Azure Container Service cluster, you need to connect to the cluster to deploy and manage workloads.</span></span> <span data-ttu-id="d5d3b-103">이 문서에서는 원격 컴퓨터에서 클러스터의 마스터 VM에 연결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-103">This article describes how to connect to the master VM of the cluster from a remote computer.</span></span> 

<span data-ttu-id="d5d3b-104">Kubernetes, DC/OS 및 Docker Swarm 클러스터는 HTTP 끝점을 로컬로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-104">The Kubernetes, DC/OS, and Docker Swarm clusters provide HTTP endpoints locally.</span></span> <span data-ttu-id="d5d3b-105">Kubernetes의 경우 이 끝점은 안전하게 인터넷에 노출되고 인터넷에 연결된 모든 컴퓨터에서 `kubectl` 명령줄 도구를 실행하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-105">For Kubernetes, this endpoint is securely exposed on the internet, and you can access it by running the `kubectl` command-line tool from any internet-connected machine.</span></span> 

<span data-ttu-id="d5d3b-106">DC/OS 및 Docker Swarm의 경우 로컬 컴퓨터에서 클러스터 관리 시스템으로 SSH(보안 셸) 터널을 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-106">For DC/OS and Docker Swarm, we recommend that you create a secure shell (SSH) tunnel from your local computer to the cluster management system.</span></span> <span data-ttu-id="d5d3b-107">터널이 설정되면 HTTP 끝점을 사용하는 명령을 실행하고 로컬 시스템에서 Orchestrator의 웹 인터페이스(제공되는 경우)를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-107">After the tunnel is established, you can run commands which use the HTTP endpoints and view the orchestrator's web interface (if available) from your local system.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d5d3b-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="d5d3b-108">Prerequisites</span></span>

* <span data-ttu-id="d5d3b-109">[Azure Container Service에 배포된](../articles/container-service/dcos-swarm/container-service-deployment.md) Kubernetes, DC/OS 또는 Docker Swarm 클러스터.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-109">A Kubernetes, DC/OS, or Docker Swarm cluster [deployed in Azure Container Service](../articles/container-service/dcos-swarm/container-service-deployment.md).</span></span>
* <span data-ttu-id="d5d3b-110">배포 중에 클러스터에 추가된 공개 키에 해당하는 SSH RSA 개인 키 파일.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-110">SSH RSA private key file, corresponding to the public key added to the cluster during deployment.</span></span> <span data-ttu-id="d5d3b-111">이러한 명령은 개인 SSH 키가 사용자의 컴퓨터의 `$HOME/.ssh/id_rsa`에 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-111">These commands assume that the private SSH key is in `$HOME/.ssh/id_rsa` on your computer.</span></span> <span data-ttu-id="d5d3b-112">자세한 내용은 [macOS 및 Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) 또는 [Windows](../articles/virtual-machines/linux/ssh-from-windows.md)에 대한 다음 지침을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-112">See these instructions for [macOS and Linux](../articles/virtual-machines/linux/mac-create-ssh-keys.md) or [Windows](../articles/virtual-machines/linux/ssh-from-windows.md) for more information.</span></span> <span data-ttu-id="d5d3b-113">SSH 연결이 작동하지 않는 경우 [SSH 키를 재설정](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md)해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-113">If the SSH connection isn't working, you may need to [reset your SSH keys](../articles/virtual-machines/linux/troubleshoot-ssh-connection.md).</span></span>

## <a name="connect-to-a-kubernetes-cluster"></a><span data-ttu-id="d5d3b-114">Kubernetes 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="d5d3b-114">Connect to a Kubernetes cluster</span></span>

<span data-ttu-id="d5d3b-115">다음 단계에 따라 컴퓨터에 `kubectl`을 설치하고 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-115">Follow these steps to install and configure `kubectl` on your computer.</span></span>

> [!NOTE] 
> <span data-ttu-id="d5d3b-116">Linux 또는 macOS에서 `sudo`을 사용하여 이 섹션의 명령을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-116">On Linux or macOS, you might need to run the commands in this section using `sudo`.</span></span>
> 

### <a name="install-kubectl"></a><span data-ttu-id="d5d3b-117">kubectl 설치</span><span class="sxs-lookup"><span data-stu-id="d5d3b-117">Install kubectl</span></span>
<span data-ttu-id="d5d3b-118">이 도구를 설치하는 한 가지 방법은 `az acs kubernetes install-cli` Azure CLI 2.0 명령을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-118">One way to install this tool is to use the `az acs kubernetes install-cli` Azure CLI 2.0 command.</span></span> <span data-ttu-id="d5d3b-119">이 명령을 실행하려면 최신 Azure CLI 2.0을 [설치](/cli/azure/install-az-cli2)하고 Azure 계정(`az login`)에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-119">To run this command, make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an Azure account (`az login`).</span></span>

```azurecli
# Linux or macOS
az acs kubernetes install-cli [--install-location=/some/directory/kubectl]

# Windows
az acs kubernetes install-cli [--install-location=C:\some\directory\kubectl.exe]
```

<span data-ttu-id="d5d3b-120">또는 [Kubernetes 릴리스 페이지](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md)에서 최신 `kubectl` 클라이언트를 직접 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-120">Alternatively, you can download the latest `kubectl` client directly from the [Kubernetes releases page](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md).</span></span> <span data-ttu-id="d5d3b-121">자세한 내용은 [kubectl 설치 및 설정](https://kubernetes.io/docs/tasks/kubectl/install/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-121">For more information, see [Installing and Setting up kubectl](https://kubernetes.io/docs/tasks/kubectl/install/).</span></span>

### <a name="download-cluster-credentials"></a><span data-ttu-id="d5d3b-122">클러스터 자격 증명 다운로드</span><span class="sxs-lookup"><span data-stu-id="d5d3b-122">Download cluster credentials</span></span>
<span data-ttu-id="d5d3b-123">일단 `kubectl`을 설치하면 클러스터 자격 증명을 컴퓨터에 복사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-123">Once you have `kubectl` installed, you need to copy the cluster credentials to your machine.</span></span> <span data-ttu-id="d5d3b-124">자격 증명을 가져오는 방법은 `az acs kubernetes get-credentials` 명령을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-124">One way to do get the credentials is with the `az acs kubernetes get-credentials` command.</span></span> <span data-ttu-id="d5d3b-125">리소스 그룹의 이름과 컨테이너 서비스 리소스의 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-125">Pass the name of the resource group and the name of the container service resource:</span></span>

```azurecli
az acs kubernetes get-credentials --resource-group=<cluster-resource-group> --name=<cluster-name>
```

<span data-ttu-id="d5d3b-126">이 명령은 클러스터 자격 증명을 `$HOME/.kube/config`로 다운로드합니다. 해당 항목은 `kubectl`에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-126">This command downloads the cluster credentials to `$HOME/.kube/config`, where `kubectl` expects it to be located.</span></span>

<span data-ttu-id="d5d3b-127">또는 `scp`을 사용하여 마스터 VM의 `$HOME/.kube/config`에서 로컬 컴퓨터로 파일을 안전하게 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-127">Alternatively, you can use `scp` to securely copy the file from `$HOME/.kube/config` on the master VM to your local machine.</span></span> <span data-ttu-id="d5d3b-128">예:</span><span class="sxs-lookup"><span data-stu-id="d5d3b-128">For example:</span></span>

```bash
mkdir $HOME/.kube
scp azureuser@<master-dns-name>:.kube/config $HOME/.kube/config
```

<span data-ttu-id="d5d3b-129">Windows에서 작업하는 경우 Windows, PuTTy 보안 파일 복사 클라이언트 또는 유사한 도구의 Ubuntu에서 Bash를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-129">If you are on Windows, you can use Bash on Ubuntu on Windows, the PuTTy secure file copy client, or a similar tool.</span></span>

### <a name="use-kubectl"></a><span data-ttu-id="d5d3b-130">kubectl 사용</span><span class="sxs-lookup"><span data-stu-id="d5d3b-130">Use kubectl</span></span>

<span data-ttu-id="d5d3b-131">`kubectl`를 구성한 경우 클러스터의 노드를 나열하여 연결을 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-131">Once you have `kubectl` configured, test the connection by listing the nodes in your cluster:</span></span>

```bash
kubectl get nodes
```

<span data-ttu-id="d5d3b-132">다른 `kubectl` 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-132">You can try other `kubectl` commands.</span></span> <span data-ttu-id="d5d3b-133">예를 들어, Kubernetes 대시보드를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-133">For example, you can view the Kubernetes Dashboard.</span></span> <span data-ttu-id="d5d3b-134">먼저 Kubernetes API 서버에 대한 프록시를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-134">First, run a proxy to the Kubernetes API server:</span></span>

```bash
kubectl proxy
```

<span data-ttu-id="d5d3b-135">이제 Kubernetes UI는 `http://localhost:8001/ui`에서 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-135">The Kubernetes UI is now available at: `http://localhost:8001/ui`.</span></span>

<span data-ttu-id="d5d3b-136">자세한 내용은 [Kubernetes 빠른 시작](http://kubernetes.io/docs/user-guide/quick-start/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-136">For more information, see the [Kubernetes quick start](http://kubernetes.io/docs/user-guide/quick-start/).</span></span>

## <a name="connect-to-a-dcos-or-swarm-cluster"></a><span data-ttu-id="d5d3b-137">DC/OS 또는 Swarm 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="d5d3b-137">Connect to a DC/OS or Swarm cluster</span></span>

<span data-ttu-id="d5d3b-138">Azure Container Service에서 배포하는 DC/OS 및 Docker Swarm 클러스터를 사용하려면 다음 지침에 따라 로컬 Linux, macOS 또는 Windows 시스템에서 SSH 터널을 만드세요.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-138">To use the DC/OS and Docker Swarm clusters deployed by Azure Container Service, follow these instructions to create a SSH tunnel from your local Linux, macOS, or Windows system.</span></span> 

> [!NOTE]
> <span data-ttu-id="d5d3b-139">이러한 지침은 SSH를 통한 TCP 트래픽 터널링에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-139">These instructions focus on tunneling TCP traffic over SSH.</span></span> <span data-ttu-id="d5d3b-140">또한 내부 클러스터 관리 시스템 중 하나를 사용하여 대화형 SSH 세션을 시작할 수도 있지만 이는 권장되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-140">You can also start an interactive SSH session with one of the internal cluster management systems, but we don't recommend this.</span></span> <span data-ttu-id="d5d3b-141">내부 시스템에 직접 작업할 경우 실수로 구성을 변경할 위험이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-141">Working directly on an internal system risks inadvertent configuration changes.</span></span>  
> 

### <a name="create-an-ssh-tunnel-on-linux-or-macos"></a><span data-ttu-id="d5d3b-142">Linux 또는 macOS에서 SSH 터널 만들기</span><span class="sxs-lookup"><span data-stu-id="d5d3b-142">Create an SSH tunnel on Linux or macOS</span></span>
<span data-ttu-id="d5d3b-143">Linux 또는 macOS에서 SSH 터널을 만들 때 가장 먼저 수행할 작업은 부하 분산된 마스터의 공용 DNS 이름을 찾는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-143">The first thing that you do when you create an SSH tunnel on Linux or macOS is to locate the public DNS name of the load-balanced masters.</span></span> <span data-ttu-id="d5d3b-144">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-144">Follow these steps:</span></span>


1. <span data-ttu-id="d5d3b-145">[Azure Portal](https://portal.azure.com)에서 컨테이너 서비스 클러스터를 포함하는 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-145">In the [Azure portal](https://portal.azure.com), browse to the resource group containing your container service cluster.</span></span> <span data-ttu-id="d5d3b-146">리소스 그룹을 확장하여 각 리소스가 표시되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-146">Expand the resource group so that each resource is displayed.</span></span> 

2. <span data-ttu-id="d5d3b-147">**컨테이너 서비스** 리소스를 클릭하고 **개요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-147">Click the **Container service** resource, and click **Overview**.</span></span> <span data-ttu-id="d5d3b-148">**Essentials(필수 정보)** 아래에 클러스터의 **마스터 FQDN**이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-148">The **Master FQDN** of the cluster appears under **Essentials**.</span></span> <span data-ttu-id="d5d3b-149">이 이름은 나중에 사용되므로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-149">Save this name for later use.</span></span> 

    ![공용 DNS 이름](./media/container-service-connect/pubdns.png)

    <span data-ttu-id="d5d3b-151">또는 컨테이너 서비스에 `az acs show` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-151">Alternatively, run the `az acs show` command on your container service.</span></span> <span data-ttu-id="d5d3b-152">명령 출력에서 **Master Profile:fqdn** 속성을 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-152">Look for the **Master Profile:fqdn** property in the command output.</span></span>

3. <span data-ttu-id="d5d3b-153">이제 셸을 열고 다음 값을 지정하여 `ssh` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-153">Now open a shell and run the `ssh` command by specifying the following values:</span></span> 

    <span data-ttu-id="d5d3b-154">**LOCAL_PORT**는 연결할 터널의 서비스 측 TCP 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-154">**LOCAL_PORT** is the TCP port on the service side of the tunnel to connect to.</span></span> <span data-ttu-id="d5d3b-155">Swarm의 경우 2375로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-155">For Swarm, set this to 2375.</span></span> <span data-ttu-id="d5d3b-156">DC/OS의 경우 80으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-156">For DC/OS, set this to 80.</span></span> 
    <span data-ttu-id="d5d3b-157">**REMOTE_PORT**는 노출하려는 끝점의 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-157">**REMOTE_PORT** is the port of the endpoint that you want to expose.</span></span> <span data-ttu-id="d5d3b-158">Swarm의 경우 2375 포트를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-158">For Swarm, use port 2375.</span></span> <span data-ttu-id="d5d3b-159">DC/OS의 경우 포트 80을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-159">For DC/OS, use port 80.</span></span>  
    <span data-ttu-id="d5d3b-160">**USERNAME** 은 클러스터를 배포할 때 제공된 사용자 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-160">**USERNAME** is the user name that was provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="d5d3b-161">**DNSPREFIX** 는 클러스터를 배포할 때 제공한 DNS 접두사입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-161">**DNSPREFIX** is the DNS prefix that you provided when you deployed the cluster.</span></span>  
    <span data-ttu-id="d5d3b-162">**REGION** 은 리소스 그룹이 있는 하위 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-162">**REGION** is the region in which your resource group is located.</span></span>  
    <span data-ttu-id="d5d3b-163">**PATH_TO_PRIVATE_KEY** [선택 사항]은 클러스터를 만들 때 제공한 공개 키에 해당하는 개인 키에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-163">**PATH_TO_PRIVATE_KEY** [OPTIONAL] is the path to the private key that corresponds to the public key you provided when you created the cluster.</span></span> <span data-ttu-id="d5d3b-164">`-i` 플래그와 함께 이 옵션을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-164">Use this option with the `-i` flag.</span></span>

    ```bash
    ssh -fNL LOCAL_PORT:localhost:REMOTE_PORT -p 2200 [USERNAME]@[DNSPREFIX]mgmt.[REGION].cloudapp.azure.com
    ```
  
  > [!NOTE]
  > <span data-ttu-id="d5d3b-165">SSH 연결 포트는 표준 포트 22가 아니라 2200입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-165">The SSH connection port is 2200 and not the standard port 22.</span></span> <span data-ttu-id="d5d3b-166">둘 이상의 마스터 VM을 포함한 클러스터에서 첫 번째 마스터 VM에 대한 연결 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-166">In a cluster with more than one master VM, this is the connection port to the first master VM.</span></span>
  > 

  <span data-ttu-id="d5d3b-167">이 명령은 출력 없이 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-167">The command returns without output.</span></span>

<span data-ttu-id="d5d3b-168">다음 섹션에서는 DC/OS 및 Swarm에 대한 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-168">See the examples for DC/OS and Swarm in the following sections.</span></span>    

### <a name="dcos-tunnel"></a><span data-ttu-id="d5d3b-169">DC/OS 터널</span><span class="sxs-lookup"><span data-stu-id="d5d3b-169">DC/OS tunnel</span></span>
<span data-ttu-id="d5d3b-170">DC/OS 끝점에 대한 터널을 열려면 다음과 같은 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-170">To open a tunnel for DC/OS endpoints, run a command like the following:</span></span>

```bash
sudo ssh -fNL 80:localhost:80 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com 
```

> [!NOTE]
> <span data-ttu-id="d5d3b-171">포트 80에 바인딩하는 다른 로컬 프로세스가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-171">Ensure that you do not have another local process that binds port 80.</span></span> <span data-ttu-id="d5d3b-172">필요한 경우 포트 80이 아닌 다른 로컬 포트(예: 포트 8080)를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-172">If necessary, you can specify a local port other than port 80, such as port 8080.</span></span> <span data-ttu-id="d5d3b-173">그러나 이 포트를 사용할 경우 일부 웹 UI 링크가 작동하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-173">However, some web UI links might not work when you use this port.</span></span>
>

<span data-ttu-id="d5d3b-174">이제 로컬 시스템에서 다음 URL을 통해 DC/OS 끝점에 액세스할 수 있습니다(로컬 포트 80 사용 시).</span><span class="sxs-lookup"><span data-stu-id="d5d3b-174">You can now access the DC/OS endpoints from your local system through the following URLs (assuming local port 80):</span></span>

* <span data-ttu-id="d5d3b-175">DC/OS: `http://localhost:80/`</span><span class="sxs-lookup"><span data-stu-id="d5d3b-175">DC/OS: `http://localhost:80/`</span></span>
* <span data-ttu-id="d5d3b-176">Marathon: `http://localhost:80/marathon`</span><span class="sxs-lookup"><span data-stu-id="d5d3b-176">Marathon: `http://localhost:80/marathon`</span></span>
* <span data-ttu-id="d5d3b-177">Mesos: `http://localhost:80/mesos`</span><span class="sxs-lookup"><span data-stu-id="d5d3b-177">Mesos: `http://localhost:80/mesos`</span></span>

<span data-ttu-id="d5d3b-178">마찬가지로, 각 응용 프로그램에 대한 rest API는 이 터널을 통해 도달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-178">Similarly, you can reach the rest APIs for each application through this tunnel.</span></span>

### <a name="swarm-tunnel"></a><span data-ttu-id="d5d3b-179">Swarm 터널</span><span class="sxs-lookup"><span data-stu-id="d5d3b-179">Swarm tunnel</span></span>
<span data-ttu-id="d5d3b-180">Swarm 끝점에 대한 터널을 열려면 다음과 같은 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-180">To open a tunnel to the Swarm endpoint, run a command like the following:</span></span>

```bash
ssh -fNL 2375:localhost:2375 -p 2200 azureuser@acsexamplemgmt.japaneast.cloudapp.azure.com
```
> [!NOTE]
> <span data-ttu-id="d5d3b-181">포트 2375에 바인딩하는 다른 로컬 프로세스가 없는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-181">Ensure that you do not have another local process that binds port 2375.</span></span> <span data-ttu-id="d5d3b-182">예를 들어 Docker 데몬을 로컬로 실행 중인 경우 기본적으로 포트 2375를 사용하도록 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-182">For example, if you are running the Docker daemon locally, it's set by default to use port 2375.</span></span> <span data-ttu-id="d5d3b-183">필요한 경우 포트 2375가 아닌 다른 로컬 포트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-183">If necessary, you can specify a local port other than port 2375.</span></span>
>

<span data-ttu-id="d5d3b-184">이제 로컬 시스템에서 Docker CLI(Docker 명령줄 인터페이스)를 사용하여 Docker Swarm 클러스터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-184">Now you can access the Docker Swarm cluster using the Docker command-line interface (Docker CLI) on your local system.</span></span> <span data-ttu-id="d5d3b-185">설치 지침은 [Docker 설치](https://docs.docker.com/engine/installation/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-185">For installation instructions, see [Install Docker](https://docs.docker.com/engine/installation/).</span></span>

<span data-ttu-id="d5d3b-186">DOCKER_HOST 환경 변수를 터널에 대해 구성한 로컬 포트로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-186">Set your DOCKER_HOST environment variable to the local port you configured for the tunnel.</span></span> 

```bash
export DOCKER_HOST=:2375
```

<span data-ttu-id="d5d3b-187">Docker Swarm 클러스터로 터널링하는 Docker 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-187">Run Docker commands that tunnel to the Docker Swarm cluster.</span></span> <span data-ttu-id="d5d3b-188">예:</span><span class="sxs-lookup"><span data-stu-id="d5d3b-188">For example:</span></span>

```bash
docker info
```

### <a name="create-an-ssh-tunnel-on-windows"></a><span data-ttu-id="d5d3b-189">Windows에서 SSH 터널 만들기</span><span class="sxs-lookup"><span data-stu-id="d5d3b-189">Create an SSH tunnel on Windows</span></span>
<span data-ttu-id="d5d3b-190">Windows에서 SSH 터널을 만드는 방법은 여러 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-190">There are multiple options for creating SSH tunnels on Windows.</span></span> <span data-ttu-id="d5d3b-191">Windows 또는 유사한 도구의 Ubuntu에서 Bash를 실행하는 경우 이 문서의 앞부분에 표시된 macOS 및 Linux에 대한 SSH 터널링 지침을 따르면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-191">If you are running Bash on Ubuntu on Windows or a similar tool, you can follow the SSH tunneling instructions shown earlier in this article for macOS and Linux.</span></span> <span data-ttu-id="d5d3b-192">Windows 사용자를 위한 대안으로, 이 섹션에서는 PuTTY를 사용하여 터널을 만드는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-192">As an alternative on Windows, this section describes how to use PuTTY to create the tunnel.</span></span>

1. <span data-ttu-id="d5d3b-193">Windows 시스템으로 [PuTTY를 다운로드합니다](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).</span><span class="sxs-lookup"><span data-stu-id="d5d3b-193">[Download PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to your Windows system.</span></span>

2. <span data-ttu-id="d5d3b-194">응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-194">Run the application.</span></span>

3. <span data-ttu-id="d5d3b-195">클러스터 관리 사용자 이름 및 클러스터에서 첫 번째 마스터의 공용 DNS 이름으로 구성된 호스트 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-195">Enter a host name that is comprised of the cluster admin user name and the public DNS name of the first master in the cluster.</span></span> <span data-ttu-id="d5d3b-196">**호스트 이름**은 `azureuser@PublicDNSName`과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-196">The **Host Name** looks similar to `azureuser@PublicDNSName`.</span></span> <span data-ttu-id="d5d3b-197">**포트**에 2200을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-197">Enter 2200 for the **Port**.</span></span>

    ![PuTTY 구성 1](./media/container-service-connect/putty1.png)

4. <span data-ttu-id="d5d3b-199">**SSH > 인증**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-199">Select **SSH > Auth**.</span></span> <span data-ttu-id="d5d3b-200">인증을 위한 개인 키 파일(.ppk 형식)에 경로를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-200">Add a path to your private key file (.ppk format) for authentication.</span></span> <span data-ttu-id="d5d3b-201">[PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)과 같은 도구를 사용하여 클러스터를 만드는 데 사용되는 SSH 키에서 이 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-201">You can use a tool such as [PuTTYgen](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html) to generate this file from the SSH key used to create the cluster.</span></span>

    ![PuTTY 구성 2](./media/container-service-connect/putty2.png)

5. <span data-ttu-id="d5d3b-203">**SSH > 터널**을 선택하고 다음 전달된 포트를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-203">Select **SSH > Tunnels** and configure the following forwarded ports:</span></span>

    * <span data-ttu-id="d5d3b-204">**원본 포트:** DC/OS의 경우 80 또는 Swarm의 경우 2375를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-204">**Source Port:** Use 80 for DC/OS or 2375 for Swarm.</span></span>
    * <span data-ttu-id="d5d3b-205">**대상:** localhost:80(DC/OS) 또는 localhost:2375(Swarm)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-205">**Destination:** Use localhost:80 for DC/OS or localhost:2375 for Swarm.</span></span>

    <span data-ttu-id="d5d3b-206">다음 예제에서는 DC/OS에 대해 구성되었지만 Docker Swarm에 대한 구성도 이와 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-206">The following example is configured for DC/OS, but will look similar for Docker Swarm.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d5d3b-207">이 터널을 만들 때 포트 80은 사용 중이 아니어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-207">Port 80 must not be in use when you create this tunnel.</span></span>
    > 

    ![PuTTY 구성 3](./media/container-service-connect/putty3.png)

6. <span data-ttu-id="d5d3b-209">완료하면 **세션 > 저장**을 클릭하여 연결 구성을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-209">When you're finished, click **Session > Save** to save the connection configuration.</span></span>

7. <span data-ttu-id="d5d3b-210">PuTTY 세션에 연결하려면 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-210">To connect to the PuTTY session, click **Open**.</span></span> <span data-ttu-id="d5d3b-211">연결하면 PuTTY 이벤트 로그에서 포트 구성을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-211">When you connect, you can see the port configuration in the PuTTY event log.</span></span>

    ![PuTTY 이벤트 로그](./media/container-service-connect/putty4.png)

<span data-ttu-id="d5d3b-213">DC/OS에 터널을 구성한 후에 다음에서 관련 끝점에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-213">After you've configured the tunnel for DC/OS, you can access the related endpoints at:</span></span>

* <span data-ttu-id="d5d3b-214">DC/OS: `http://localhost/`</span><span class="sxs-lookup"><span data-stu-id="d5d3b-214">DC/OS: `http://localhost/`</span></span>
* <span data-ttu-id="d5d3b-215">Marathon: `http://localhost/marathon`</span><span class="sxs-lookup"><span data-stu-id="d5d3b-215">Marathon: `http://localhost/marathon`</span></span>
* <span data-ttu-id="d5d3b-216">Mesos: `http://localhost/mesos`</span><span class="sxs-lookup"><span data-stu-id="d5d3b-216">Mesos: `http://localhost/mesos`</span></span>

<span data-ttu-id="d5d3b-217">Docker Swarm에 대한 터널을 구성한 후에 Windows 설정을 열고 `DOCKER_HOST` 값을 가진 `:2375`(이)라는 시스템 환경 변수를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-217">After you've configured the tunnel for Docker Swarm, open your Windows settings to configure a system environment variable named `DOCKER_HOST` with a value of `:2375`.</span></span> <span data-ttu-id="d5d3b-218">그런 다음 Docker CLI를 통해 Swarm 클러스터에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-218">Then, you can access the Swarm cluster through the Docker CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5d3b-219">다음 단계</span><span class="sxs-lookup"><span data-stu-id="d5d3b-219">Next steps</span></span>
<span data-ttu-id="d5d3b-220">클러스터에서 컨테이너를 배포하고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d5d3b-220">Deploy and manage containers in your cluster:</span></span>

* [<span data-ttu-id="d5d3b-221">Azure Container Service 및 Kubernetes로 작업</span><span class="sxs-lookup"><span data-stu-id="d5d3b-221">Work with Azure Container Service and Kubernetes</span></span>](../articles/container-service/kubernetes/container-service-kubernetes-ui.md)
* [<span data-ttu-id="d5d3b-222">Azure 컨테이너 서비스 및 DC/OS로 작업</span><span class="sxs-lookup"><span data-stu-id="d5d3b-222">Work with Azure Container Service and DC/OS</span></span>](../articles/container-service//dcos-swarm/container-service-mesos-marathon-rest.md)
* [<span data-ttu-id="d5d3b-223">Azure 컨테이너 서비스 및 Docker Swarm으로 작업</span><span class="sxs-lookup"><span data-stu-id="d5d3b-223">Work with the Azure Container Service and Docker Swarm</span></span>](../articles//container-service/dcos-swarm/container-service-docker-swarm.md)

