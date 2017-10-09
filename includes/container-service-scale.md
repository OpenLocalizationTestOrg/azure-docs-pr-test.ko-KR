# <a name="scale-agent-nodes-in-a-container-service-cluster"></a>Container Service 클러스터의 에이전트 노드 수 변경
후 [Azure 컨테이너 서비스 클러스터 배포](../articles/container-service/dcos-swarm/container-service-deployment.md), 에이전트 노드의 toochange hello 수를 할 수 있습니다. 예를 들어 더 많은 컨테이너 응용 프로그램 또는 인스턴스를 실행하기 위해 더 많은 에이전트가 필요할 수 있습니다. 

Azure CLI 2.0 hello 또는 hello Azure 포털을 사용 하 여 hello DC/OS, docker는 Docker Swarm 또는 Kubernetes 클러스터의 에이전트 노드 수를 변경할 수 있습니다. 

## <a name="scale-with-hello-azure-portal"></a>Azure 포털 hello 함께 크기 조정

1. Hello에 [Azure 포털](https://portal.azure.com), 찾아보기 **컨테이너 서비스**, toomodify 원하는 hello 컨테이너 서비스를 클릭 하 고 있습니다.
2. Hello에 **컨테이너 서비스** 블레이드에서 클릭 **에이전트**합니다.
3. **VM 개수**, 원하는 hello 에이전트 노드 수를 입력 합니다.

    ![Hello 포털에서 풀의 크기를 조정합니다](./media/container-service-scale/container-service-scale-portal.png)

4. toosave hello 구성 클릭 **저장**합니다.

## <a name="scale-with-hello-azure-cli-20"></a>Hello Azure CLI 2.0 함께 크기 조정

다음 사항을 확인 하면 [설치](/cli/azure/install-az-cli2) 최신 Azure CLI 2.0 hello 및 tooan 로그인 azure 계정 (`az login`).

### <a name="see-hello-current-agent-count"></a>현재 에이전트 수를 hello를 참조 하십시오.
현재 에이전트 toosee hello 수 hello 클러스터에서 실행 hello `az acs show` 명령입니다. 이 hello 클러스터 구성을 보여 줍니다. 예를 들어 다음 명령을 표시 hello 라는 hello 컨테이너 서비스의 구성을 hello `containerservice-myACSName` hello 리소스 그룹에 `myResourceGroup`:

```azurecli
az acs show -g myResourceGroup -n containerservice-myACSName
```

hello에 hello 에이전트 수를 반환 하는 hello 명령 `Count` 아래 `AgentPoolProfiles`합니다.

### <a name="use-hello-az-acs-scale-command"></a>사용 하 여 hello az acs 눈금 명령
에이전트 노드를 hello 실행 toochange hello 수 `az acs scale` 명령 및 공급 hello **리소스 그룹**, **컨테이너 서비스 이름을**, 및 필요한 hello **새 에이전트 수**. 더 작은 숫자를 사용하여 규모를 축소하거나 더 큰 숫자를 사용하여 규모를 확장할 수 있습니다.

예를 들어, 에이전트에 hello 이전 하는 클러스터 too10 toochange hello 수 hello 다음 명령을 입력 합니다.

```azurecli
az acs scale -g myResourceGroup -n containerservice-myACSName --new-agent-count 10
```

hello Azure CLI 2.0 hello hello 새 에이전트 수를 포함 하 여 hello 컨테이너 서비스의 새 구성을 나타내는 JSON 문자열을 반환 합니다.

자세한 명령 옵션을 보려면 `az acs scale --help`를 실행합니다.

## <a name="scaling-considerations"></a>규모 조정 고려 사항

* hello 에이전트 노드 수는 1부터 100 사이 여야 합니다. 

* 코어 할당량 hello 클러스터의 에이전트 노드 수를 제한할 수 있습니다.

* 에이전트 노드 크기 조정 작업은 적용된 tooan Azure 가상 컴퓨터 크기 집합 hello 에이전트 풀을 포함 합니다. DC/OS 클러스터 hello 개인 풀의 에이전트 노드만이 문서에 표시 된 hello 작업에 의해 조정 됩니다.

* 클러스터에 배포 하는 hello orchestrator를 따라 hello hello 클러스터에서 실행 중인 컨테이너의 인스턴스 개수를 별도로 확장할 수 있습니다. 예를 들어 DC/OS 클러스터를 사용 하 여 hello [마라톤 UI](../articles/container-service/dcos-swarm/container-service-mesos-marathon-ui.md) toochange hello 컨테이너 응용 프로그램의 인스턴스 수입니다.

* 현재 컨테이너 서비스 클러스터에 있는 에이전트 노드의 자동 규모 조정은 지원되지 않습니다.

## <a name="next-steps"></a>다음 단계
* Azure Container Service에서 Azure CLI 2.0 명령을 사용하는 방법에 대한 [추가 예제](../articles/container-service/dcos-swarm/container-service-create-acs-cluster-cli.md)를 참조하세요.
* Azure Container Service의 [DC/OS 에이전트 풀](../articles/container-service/dcos-swarm/container-service-dcos-agents.md)에 대해 자세히 알아보세요.

