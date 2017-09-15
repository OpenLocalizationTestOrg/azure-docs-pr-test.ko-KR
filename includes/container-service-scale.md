# <a name="scale-agent-nodes-in-a-container-service-cluster"></a><span data-ttu-id="0b0e3-101">Container Service 클러스터의 에이전트 노드 수 변경</span><span class="sxs-lookup"><span data-stu-id="0b0e3-101">Scale agent nodes in a Container Service cluster</span></span>
<span data-ttu-id="0b0e3-102">[Azure Container Service 클러스터를 배포](../articles/container-service/dcos-swarm/container-service-deployment.md)한 후 에이전트 노드의 수를 변경해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-102">After [deploying an Azure Container Service cluster](../articles/container-service/dcos-swarm/container-service-deployment.md), you might need to change the number of agent nodes.</span></span> <span data-ttu-id="0b0e3-103">예를 들어 더 많은 컨테이너 응용 프로그램 또는 인스턴스를 실행하기 위해 더 많은 에이전트가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-103">For example, you might need more agents so you can run more container applications or instances.</span></span> 

<span data-ttu-id="0b0e3-104">Azure Portal 또는 Azure CLI 2.0을 사용하여 DC/OS, Docker Swarm 또는 Kubernetes 클러스터의 에이전트 노드 수를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-104">You can change the number of agent nodes in a DC/OS, Docker Swarm, or Kubernetes cluster by using the Azure portal or the Azure CLI 2.0.</span></span> 

## <a name="scale-with-the-azure-portal"></a><span data-ttu-id="0b0e3-105">Azure Portal을 사용하여 규모 조정</span><span class="sxs-lookup"><span data-stu-id="0b0e3-105">Scale with the Azure portal</span></span>

1. <span data-ttu-id="0b0e3-106">[Azure Portal](https://portal.azure.com)에서 **컨테이너 서비스**를 찾아본 후 수정하고자 하는 컨테이너 서비스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-106">In the [Azure portal](https://portal.azure.com), browse for **Container services**, and then click the container service that you want to modify.</span></span>
2. <span data-ttu-id="0b0e3-107">**컨테이너 서비스** 블레이드에서 **에이전트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-107">In the **Container service** blade, click **Agents**.</span></span>
3. <span data-ttu-id="0b0e3-108">**VM 개수**에서 원하는 에이전트 노드 수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-108">In **VM Count**, enter the desired number of agents nodes.</span></span>

    ![포털에서 풀 규모 조정](./media/container-service-scale/container-service-scale-portal.png)

4. <span data-ttu-id="0b0e3-110">구성을 저장하려면 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-110">To save the configuration, click **Save**.</span></span>

## <a name="scale-with-the-azure-cli-20"></a><span data-ttu-id="0b0e3-111">Azure CLI 2.0을 사용하여 규모 조정</span><span class="sxs-lookup"><span data-stu-id="0b0e3-111">Scale with the Azure CLI 2.0</span></span>

<span data-ttu-id="0b0e3-112">최신 Azure CLI 2.0을 [설치](/cli/azure/install-az-cli2)하고 Azure 계정(`az login`)에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-112">Make sure that you [installed](/cli/azure/install-az-cli2) the latest Azure CLI 2.0 and logged in to an azure account (`az login`).</span></span>

### <a name="see-the-current-agent-count"></a><span data-ttu-id="0b0e3-113">현재 에이전트 수 확인</span><span class="sxs-lookup"><span data-stu-id="0b0e3-113">See the current agent count</span></span>
<span data-ttu-id="0b0e3-114">현재 클러스터에 있는 에이전트의 개수를 확인하려면 `az acs show` 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-114">To see the number of agents currently in the cluster, run the `az acs show` command.</span></span> <span data-ttu-id="0b0e3-115">이 명령은 클러스터 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-115">This shows the cluster configuration.</span></span> <span data-ttu-id="0b0e3-116">예를 들어, 다음 명령은 리소스 그룹 `myResourceGroup`의 `containerservice-myACSName`이라는 컨테이너 서비스의 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-116">For example, the following command shows the configuration of the container service named `containerservice-myACSName` in the resource group `myResourceGroup`:</span></span>

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

<span data-ttu-id="0b0e3-117">이 명령은 `AgentPoolProfiles` 아래 `Count` 값에 에이전트 수를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-117">The command returns the number of agents in the `Count` value under `AgentPoolProfiles`.</span></span>

### <a name="use-the-az-acs-scale-command"></a><span data-ttu-id="0b0e3-118">az acs scale 명령 사용</span><span class="sxs-lookup"><span data-stu-id="0b0e3-118">Use the az acs scale command</span></span>
<span data-ttu-id="0b0e3-119">에이전트 노드 수를 변경하려면 `az acs scale` 명령을 실행하고 **리소스 그룹**, **컨테이너 서비스 이름** 및 원하는 **새 에이전트 수**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-119">To change the number of agent nodes, run the `az acs scale` command and supply the **resource group**, **container service name**, and the desired **new agent count**.</span></span> <span data-ttu-id="0b0e3-120">더 작은 숫자를 사용하여 규모를 축소하거나 더 큰 숫자를 사용하여 규모를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-120">By using a smaller or higher number, you can scale down or up, respectively.</span></span>

<span data-ttu-id="0b0e3-121">예를 들어, 이전 클러스터에서 에이전트 수를 10으로 변경하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-121">For example, to change the number of agents in the previous cluster to 10, type the following command:</span></span>

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

<span data-ttu-id="0b0e3-122">Azure CLI 2.0에서는 새 에이전트 수를 포함한 컨테이너 서비스의 새 구성을 나타내는 JSON 문자열을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-122">The Azure CLI 2.0 returns a JSON string representing the new configuration of the container service, including the new agent count.</span></span>

<span data-ttu-id="0b0e3-123">자세한 명령 옵션을 보려면 `az acs scale --help`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-123">For more command options, run `az acs scale --help`.</span></span>

## <a name="scaling-considerations"></a><span data-ttu-id="0b0e3-124">규모 조정 고려 사항</span><span class="sxs-lookup"><span data-stu-id="0b0e3-124">Scaling considerations</span></span>

* <span data-ttu-id="0b0e3-125">에이전트 노드 수는 1에서 100(포함) 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-125">The number of agent nodes must be between 1 and 100, inclusive.</span></span> 

* <span data-ttu-id="0b0e3-126">코어 할당량에 따라 클러스터의 에이전트 노드 수가 제한될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-126">Your cores quota can limit the number of agent nodes in a cluster.</span></span>

* <span data-ttu-id="0b0e3-127">에이전트 노드 규모 조정 작업은 에이전트 풀을 포함하는 Azure 가상 컴퓨터 확장 집합에 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-127">Agent node scaling operations are applied to an Azure virtual machine scale set that contains the agent pool.</span></span> <span data-ttu-id="0b0e3-128">DC/OS 클러스터의 경우 이 문서에 나와 있는 작업으로 개인 풀의 에이전트 노드의 크기만 조정됩니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-128">In a DC/OS cluster, only agent nodes in the private pool are scaled by the operations shown in this article.</span></span>

* <span data-ttu-id="0b0e3-129">클러스터에서 배포하는 조정자에 따라 클러스터에서 실행되는 컨테이너의 인스턴스 수를 개별적으로 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-129">Depending on the orchestrator you deploy in your cluster, you can separately scale the number of instances of a container running on the cluster.</span></span> <span data-ttu-id="0b0e3-130">예를 들어, DC/OS 클러스터의 경우 [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md)를 사용하여 컨테이너 응용 프로그램의 인스턴스 수를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-130">For example, in a DC/OS cluster, use the [Marathon UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) to change the number of instances of a container application.</span></span>

* <span data-ttu-id="0b0e3-131">현재 컨테이너 서비스 클러스터에 있는 에이전트 노드의 자동 규모 조정은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-131">Currently, autoscaling of agent nodes in a container service cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b0e3-132">다음 단계</span><span class="sxs-lookup"><span data-stu-id="0b0e3-132">Next steps</span></span>
* <span data-ttu-id="0b0e3-133">Azure Container Service에서 Azure CLI 2.0 명령을 사용하는 방법에 대한 [추가 예제](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-133">See [more examples](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md) of using Azure CLI 2.0 commands with Azure Container Service.</span></span>
* <span data-ttu-id="0b0e3-134">Azure Container Service의 [DC/OS 에이전트 풀](../articles/container-service/dcos-swarm/container-service-dcos-agents.md)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="0b0e3-134">Learn more about [DC/OS agent pools](../articles/container-service/dcos-swarm/container-service-dcos-agents.md) in Azure Container Service.</span></span>

