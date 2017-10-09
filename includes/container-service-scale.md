# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="89bab-101">Container Service 클러스터의 에이전트 노드 수 변경</span><span class="sxs-lookup"><span data-stu-id="89bab-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="89bab-102">후 [Azure 컨테이너 서비스 클러스터 배포](../articles/container-service/dcos-swarm/container-service-deployment.md), 에이전트 노드의 toochange hello 수를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need toochange hello number of agent nodes.</span></span> <span data-ttu-id="89bab-103">예를 들어 더 많은 컨테이너 응용 프로그램 또는 인스턴스를 실행하기 위해 더 많은 에이전트가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="89bab-104">Azure CLI 2.0 hello 또는 hello Azure 포털을 사용 하 여 hello DC/OS, docker는 Docker Swarm 또는 Kubernetes 클러스터의 에이전트 노드 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-104">You can change hello number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using hello Azure portal or hello Azure CLI 2.0.</span></span> 

## <a name="scale-with-hello-azure-portal"></a><span data-ttu-id="89bab-105">Azure 포털 hello 함께 크기 조정</span><span class="sxs-lookup"><span data-stu-id="89bab-105">Scale with hello Azure portal</span></span>

1. <span data-ttu-id="89bab-106">Hello에 [Azure 포털](https://portal.azure.com), 찾아보기 **컨테이너 서비스**, toomodify 원하는 hello 컨테이너 서비스를 클릭 하 고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-106">In hello [Azure portal](https://portal.azure.com), browse for **Container services**, and then click hello container service that you want toomodify.</span></span>
2. <span data-ttu-id="89bab-107">Hello에 **컨테이너 서비스** 블레이드에서 클릭 **에이전트**합니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-107">In hello **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="89bab-108">**VM 개수**, 원하는 hello 에이전트 노드 수를 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-108">In **VM Count**, enter hello desired number of agents nodes.</span></span>

    ![Hello 포털에서 풀의 크기를 조정합니다](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="89bab-110">toosave hello 구성 클릭 **저장**합니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-110">toosave hello configuration, click **Save**.</span></span>

## <a name="scale-with-hello-azure-cli-20"></a><span data-ttu-id="89bab-111">Hello Azure CLI 2.0 함께 크기 조정</span><span class="sxs-lookup"><span data-stu-id="89bab-111">Scale with hello Azure CLI 2.0</span></span>

<span data-ttu-id="89bab-112">다음 사항을 확인 하면 [설치](/cli/azure/install-az-cli2) 최신 Azure CLI 2.0 hello 및 tooan 로그인 azure 계정 (`az login`).</span><span class="sxs-lookup"><span data-stu-id="89bab-112">Make sure that you [installed](/cli/azure/install-az-cli2) hello latest Azure CLI 2.0 and logged in tooan azure account (`az login`).</span></span>

### <a name="see-hello-current-agent-count"></a><span data-ttu-id="89bab-113">현재 에이전트 수를 hello를 참조 하십시오.</span><span class="sxs-lookup"><span data-stu-id="89bab-113">See hello current agent count</span></span>
<span data-ttu-id="89bab-114">현재 에이전트 toosee hello 수 hello 클러스터에서 실행 hello `az acs show` 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-114">toosee hello number of agents currently in hello cluster, run hello `az acs show` command.</span></span> <span data-ttu-id="89bab-115">이 hello 클러스터 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-115">This shows hello cluster configuration.</span></span> <span data-ttu-id="89bab-116">예를 들어 다음 명령을 표시 hello 라는 hello 컨테이너 서비스의 구성을 hello `containerservice-myACSName` hello 리소스 그룹에 `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="89bab-116">For example, hello following command shows hello configuration of hello container service named `containerservice-myACSName` in hello resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="89bab-117">hello에 hello 에이전트 수를 반환 하는 hello 명령 `Count` 아래 `AgentPoolProfiles`합니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-117">hello command returns hello number of agents in hello `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-hello-az-acs-scale-command"></a><span data-ttu-id="89bab-118">사용 하 여 hello az acs 눈금 명령</span><span class="sxs-lookup"><span data-stu-id="89bab-118">Use hello az acs scale command</span></span>
<span data-ttu-id="89bab-119">에이전트 노드를 hello 실행 toochange hello 수 `az acs scale` 명령 및 공급 hello **리소스 그룹**, **컨테이너 서비스 이름을**, 및 필요한 hello **새 에이전트 수**.</span><span class="sxs-lookup"><span data-stu-id="89bab-119">toochange hello number of agent nodes, run hello `az acs scale` command and supply hello **resource group**, **container service name**, and hello desired **new agent count**.</span></span> <span data-ttu-id="89bab-120">더 작은 숫자를 사용하여 규모를 축소하거나 더 큰 숫자를 사용하여 규모를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="89bab-121">예를 들어, 에이전트에 hello 이전 하는 클러스터 too10 toochange hello 수 hello 다음 명령을 입력 합니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-121">For example, toochange hello number of agents in hello previous cluster too10, type hello following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="89bab-122">hello Azure CLI 2.0 hello hello 새 에이전트 수를 포함 하 여 hello 컨테이너 서비스의 새 구성을 나타내는 JSON 문자열을 반환 합니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-122">hello Azure CLI 2.0 returns a JSON string representing hello new configuration of hello container service, including hello new agent count.</span></span>

<span data-ttu-id="89bab-123">자세한 명령 옵션을 보려면 `az acs scale --help`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="89bab-124">규모 조정 고려 사항</span><span class="sxs-lookup"><span data-stu-id="89bab-124">Scaling considerations</span></span>

* <span data-ttu-id="89bab-125">hello 에이전트 노드 수는 1부터 100 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-125">hello number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="89bab-126">코어 할당량 hello 클러스터의 에이전트 노드 수를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-126">Your cores quota can limit hello number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="89bab-127">에이전트 노드 크기 조정 작업은 적용된 tooan Azure 가상 컴퓨터 크기 집합 hello 에이전트 풀을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-127">Agent node scaling operations are applied tooan Azure virtual machine scale set that contains hello agent pool.</span></span> <span data-ttu-id="89bab-128">DC/OS 클러스터 hello 개인 풀의 에이전트 노드만이 문서에 표시 된 hello 작업에 의해 조정 됩니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-128">In a DC/OS cluster, only agent nodes in hello private pool are scaled by hello operations shown in this article.</span></span>

* <span data-ttu-id="89bab-129">클러스터에 배포 하는 hello orchestrator를 따라 hello hello 클러스터에서 실행 중인 컨테이너의 인스턴스 개수를 별도로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-129">Depending on hello orchestrator you deploy in your cluster, you can separately scale hello number of instances of a container running on hello cluster.</span></span> <span data-ttu-id="89bab-130">예를 들어 DC/OS 클러스터를 사용 하 여 hello [마라톤 UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello 컨테이너 응용 프로그램의 인스턴스 수입니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-130">For example, in a DC/OS cluster, use hello [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello number of instances of a container application.</span></span>

* <span data-ttu-id="89bab-131">현재 컨테이너 서비스 클러스터에 있는 에이전트 노드의 자동 규모 조정은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="89bab-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="89bab-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="89bab-132">Next steps</span></span>
* <span data-ttu-id="89bab-133">Azure Container Service에서 Azure CLI 2.0 명령을 사용하는 방법에 대한 [추가 예제](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="89bab-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="89bab-134">Azure Container Service의 [DC/OS 에이전트 풀](../articles/container-service/dcos-swarm/container-service-dcos-agents.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="89bab-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

