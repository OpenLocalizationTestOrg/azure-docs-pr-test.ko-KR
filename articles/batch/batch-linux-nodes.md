---
title: "가상 컴퓨터에 Linux aaaRun 계산 노드-Azure 일괄 처리 | Microsoft Docs"
description: "어떻게 tooprocess 프로그램 병렬 계산 작업에 알아봅니다. Azure 일괄 처리에서 Linux 가상 컴퓨터의 풀입니다."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>Batch 풀에서 Linux 계산 노드 프로비전

Linux 및 Windows 가상 컴퓨터에서 Azure 배치 toorun 병렬 계산 작업을 사용할 수 있습니다. 이 문서에서는 linux toocreate 풀 두 hello를 사용 하 여 hello 일괄 처리 서비스의 노드를 계산 하는 방법을 자세히 설명 [일괄 처리 Python] [ py_batch_package] 및 [일괄 처리.NET] [ api_net] 클라이언트 라이브러리입니다.

> [!NOTE]
> 응용 프로그램 패키지는 2017년 7월 5일 이후에 만들어진 모든 Batch 풀에서 지원됩니다. 클라우드 서비스 구성을 사용 하 여 hello 풀이 작성 되었습니다. 경우에 10 2016 년 3 월 사이의 5 년 7 월 2017 생성 되는 일괄 처리 풀에서 사용할 수 있습니다. 2016 년 3 월 이전 too10를 생성 하는 일괄 처리 풀에서 응용 프로그램 패키지를 지원 하지 않습니다. 응용 프로그램 tooyour 일괄 처리 노드 toodeploy 패키지 하는 응용 프로그램을 사용 하는 방법에 대 한 자세한 내용은 참조 [일괄 처리 응용 프로그램 패키지와 응용 프로그램 toocompute 노드를 배포할](batch-application-packages.md)합니다.
>
>

## <a name="virtual-machine-configuration"></a>가상 컴퓨터 구성
일괄 처리의 계산 노드는 풀을 만들 때 두 가지 옵션이 있습니다 tooselect hello 노드 크기 및 운영 체제: 클라우드 서비스 구성 및 가상 컴퓨터 구성.

**Cloud Services 구성**은 Windows 계산 노드 *만*제공합니다. 사용 가능한 계산 노드 크기에 나열 되어 [클라우드 서비스에 대 한 크기](../cloud-services/cloud-services-sizes-specs.md), 사용 가능한 운영 체제 hello에 나열 됩니다 [Azure 게스트 OS 릴리스 및 SDK 호환성 매트릭스](../cloud-services/cloud-services-guestos-update-matrix.md)합니다. Azure 클라우드 서비스 노드를 포함 하는 풀을 만들 때 hello 노드 크기를 지정 하 고 hello hello에서 설명 하는 OS 제품군을 앞에서 언급 한 문서. Windows 계산 노드의 풀에는 Cloud Services가 가장 일반적으로 사용됩니다.

**가상 컴퓨터 구성** 은 계산 노드에 대한 Linux와 Windows 이미지를 제공합니다. 사용 가능한 계산 노드 크기는 [Azure에서 가상 컴퓨터에 대한 크기](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)(Linux) 및 [Azure에서 가상 컴퓨터에 대한 크기](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)(Windows)에 나열되어 있습니다. 가상 컴퓨터 구성 노드를 포함 하는 풀을 만들 때 hello 노드와 hello 가상 컴퓨터 이미지 참조 hello 배치 노드 에이전트 SKU toobe hello 노드에 설치의 hello 크기를 지정 해야 합니다.

### <a name="virtual-machine-image-reference"></a>가상 컴퓨터 이미지 참조
일괄 처리 서비스는 hello [가상 컴퓨터 크기 집합](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux 노드를 계산 합니다. Hello에서 이미지를 지정할 수 [Azure 마켓플레이스][vm_marketplace], 하거나 사용자 지정 이미지를 준비한를 제공 합니다. 사용자 지정 이미지에 대한 자세한 내용은 [Batch를 사용하여 대규모 병렬 계산 솔루션 개발](batch-api-basics.md#pool)을 참조하세요.

가상 컴퓨터 이미지 참조를 구성할 때 hello 가상 컴퓨터 이미지의 hello 속성을 지정 합니다. 가상 컴퓨터 이미지 참조를 만들 때 다음과 같은 속성 hello 요소가 필요 합니다.

| **이미지 참조 속성** | **예제** |
| --- | --- |
| 게시자 |Canonical |
| 제안 |UbuntuServer |
| SKU |14.04.4-LTS |
| 버전 |최신 |

> [!TIP]
> 이러한 속성 및 toolist 마켓플레이스 이미지 방법에 대 한 자세히 알아볼 수 있습니다 [탐색 및 CLI 또는 PowerShell을 사용 하 여 Azure의 Linux 가상 컴퓨터 이미지 선택](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)합니다. 일부 Marketplace 이미지가 현재 Batch와 호환되지 않습니다. 자세한 내용은 [노드 에이전트 SKU](#node-agent-sku)를 참조하세요.
>
>

### <a name="node-agent-sku"></a>노드 에이전트 SKU
hello 배치 노드 에이전트는 hello 풀의 각 노드에서 실행 되 고 hello 노드와 hello 일괄 처리 서비스 간의 hello 명령 컨트롤 인터페이스를 제공 하는 프로그램입니다. 서로 다른 운영 체제에 대 한 Sku, 라고 hello 노드 에이전트를 다른 구현이 있습니다. 기본적으로, 가상 컴퓨터 구성을 만들 때 먼저 hello 가상 컴퓨터 이미지 참조를 지정 하 고 hello 노드 에이전트 tooinstall hello 이미지에 지정 합니다. 일반적으로 각 노드 에이전트 SKU는 여러 가상 컴퓨터 이미지와 호환됩니다. 다음은 노드 에이전트 SKU의 몇 가지 예입니다.

* batch.node.ubuntu 14.04
* batch.node.centos 7
* batch.node.windows amd64

> [!IMPORTANT]
> Hello Marketplace에서에서 사용할 수 있는 일부 가상 컴퓨터 이미지 hello 현재 사용할 수 있는 배치 노드 에이전트와 호환 됩니다. 가상 컴퓨터 이미지 서로 호환 hello 및 hello 일괄 처리 Sdk toolist hello 사용할 수 있는 노드 에이전트 Sku를 사용 합니다. Hello 참조 [목록의 가상 컴퓨터 이미지](#list-of-virtual-machine-images) 이 문서 뒷부분의 자세한 내용 및 예제는 방법에 대 한 tooretrieve 런타임에 유효한 이미지의 목록입니다.
>
>

## <a name="create-a-linux-pool-batch-python"></a>Linux 풀 만들기: Batch Python
hello 만드는 코드는 방법의 예가 toouse hello [Python에 대 한 Microsoft Azure 배치 클라이언트 라이브러리] [ py_batch_package] toocreate Ubuntu server 풀 계산 노드. 참조 설명서에서 일괄 처리 Python 모듈을 찾을 수 있습니다 hello에 대 한 [azure.batch 패키지] [ py_batch_docs] 읽기 hello 문서에 있습니다.

이 코드 조각은 명시적으로 [ImageReference][py_imagereference]를 만들고 각 속성(게시자, 제품, SKU, 버전)을 지정합니다. 하지만 프로덕션 코드에서는 권장 hello를 사용 하는 [list_node_agent_skus] [ py_list_skus] 메서드 toodetermine 및 hello 사용할 수 있는 이미지와 노드 에이전트 SKU 조합 런타임에에서 선택 합니다.

```python
# Import hello required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

앞에서 설명한 대로 좋습니다 hello를 만드는 대신 [ImageReference] [ py_imagereference] hello를 사용 하는 명시적으로 [list_node_agent_skus] [ py_list_skus] hello에서 toodynamically select 메서드는 현재 노드 에이전트/마켓플레이스 이미지 조합을 지원 합니다. Python 조각과 방법을 따르는 hello toouse이 이렇게 합니다.

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a>Linux 풀 만들기: Batch .NET
hello 만드는 코드는 방법의 예가 toouse hello [일괄 처리.NET] [ nuget_batch_net] 클라이언트 라이브러리 toocreate 풀 Ubuntu 서버에 노드를 계산 합니다. Hello를 찾을 수 있습니다 [일괄 처리.NET 참조 설명서] [ api_net] msdn 합니다.

hello 다음 코드 조각을 사용 하 여 hello [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] 현재 지원 되는 마켓플레이스 이미지와 노드 에이전트 SKU 조합을 hello 목록에서 메서드 tooselect 합니다. 이 방법은 hello 목록은 지원 되는 조합 시간 tootime에서 변경 될 수 있으므로 적합 합니다. 가장 일반적으로 지원되는 조합을 추가합니다.

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

이전 코드 조각 hello hello를 사용 하지는 않지만 [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] 방법 toodynamically 목록에서 선택 (권장) 이미지와 노드 에이전트 SKU 조합을 지원, 구성할 수도 있습니다는 [ImageReference] [ net_imagereference] 명시적으로:

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>가상 컴퓨터 이미지 목록
hello 다음 표이 문서에 마지막으로 업데이트할 때 사용할 수 있는 배치 노드 에이전트 hello와 호환 되는 hello 마켓플레이스 가상 컴퓨터 이미지입니다. 것이 중요 한 toonote는이 목록에는 최종 이미지와 노드 에이전트 추가 했거나 언제 든 제거할 수 있습니다. 일괄 처리 응용 프로그램 및 서비스 항상를 사용 하는 것이 좋습니다 [list_node_agent_skus] [ py_list_skus] (Python) 및 [ListNodeAgentSkus] [ net_list_skus] 선택한 (일괄 처리.NET) toodetermine hello 현재 사용 가능한 Sku입니다.

> [!WARNING]
> 다음 목록 hello 언제 든 지 변경 될 수 있습니다. 항상 hello를 사용 하 여 **목록 노드 에이전트 SKU** hello 일괄 처리 Api toolist에서 사용할 수 있는 방법을 hello 호환 가상 컴퓨터 및 노드 에이전트 Sku 일괄 처리 작업을 실행 합니다.
>
>

| **게시자** | **제안** | **이미지 SKU** | **버전** | **노드 에이전트 SKU ID** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canonical | UbuntuServer | 14.04.5-LTS | 최신 | batch.node.ubuntu 14.04 |
| Canonical | UbuntuServer | 16.04.0-LTS | 최신 | batch.node.ubuntu 16.04 |
| Credativ | Debian | 8 | 최신 | batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | 최신 | batch.node.centos 7 |
| OpenLogic | CentOS | 7.1 | 최신 | batch.node.centos 7 |
| OpenLogic | CentOS-HPC | 7.1 | 최신 | batch.node.centos 7 |
| OpenLogic | CentOS | 7.2 | 최신 | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7.0 | 최신 | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7.2 | 최신 | batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | 최신 | batch.node.opensuse 13.2 |
| SUSE | openSUSE-Leap | 42.1 | 최신 | batch.node.opensuse 42.1 |
| SUSE | SLES | 12-SP1 | 최신 | batch.node.opensuse 42.1 |
| SUSE | SLES-HPC | 12-SP1 | 최신 | batch.node.opensuse 42.1 |
| microsoft-ads | linux-data-science-vm | linuxdsvm | 최신 | batch.node.centos 7 |
| microsoft-ads | standard-data-science-vm | standard-data-science-vm | 최신 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2008-R2-SP1 | 최신 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-Datacenter | 최신 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-R2-Datacenter | 최신 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter | 최신 | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter-with-Containers | 최신 | batch.node.windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>SSH를 사용 하 여 tooLinux 노드를 연결 합니다.
개발 중 이나 문제를 해결 하는 동안 풀의 toohello 노드에 필요한 toosign을 알 수 있습니다. Windows 컴퓨터 노드 달리 프로토콜 RDP (원격 데스크톱) tooconnect tooLinux 노드를 사용할 수 없습니다. 대신, hello 일괄 처리 서비스에는 원격 연결에 대 한 각 노드의 SSH 액세스할을 수 있습니다.

hello 다음 Python 코드 조각에서는 사용자 원격 연결에 필요한 풀의 각 노드에서 합니다. 각 노드에 대 한 hello 보안 셸 (SSH) 연결 정보를 출력 합니다.

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

다음은 Linux 노드가 4 개를 포함 하는 풀에 대 한 hello 이전 코드에 대 한 샘플 출력이입니다.

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

노드에 사용자를 만들 때 암호 대신 SSH 공개 키를 지정할 수 있습니다. Python SDK hello에서 hello를 사용 하 여 **ssh_public_key** 매개 변수와 [ComputeNodeUser][py_computenodeuser]합니다. .NET에서는 hello를 사용 하 여 [ComputeNodeUser][net_computenodeuser].[ SshPublicKey] [ net_ssh_key] 속성입니다.

## <a name="pricing"></a>가격
Azure Batch는 Azure 클라우드 서비스 및 Azure 가상 컴퓨터 기술을 기반으로 빌드됩니다. hello 자체 일괄 처리 서비스는 hello에 대해서만 요금이 청구 되므로 의미 계산 일괄 처리 솔루션을 사용 하는 리소스는 무료로 제공 됩니다. 선택 하는 경우 **클라우드 서비스 구성**, hello에 따라 요금이 청구 되므로 [클라우드 서비스 가격] [ cloud_services_pricing] 구조입니다. 선택 하는 경우 **가상 컴퓨터 구성**, hello에 따라 요금이 청구 되므로 [가상 컴퓨터 가격] [ vm_pricing] 구조입니다. 

사용 하 여 응용 프로그램 tooyour 일괄 처리 노드를 배포 하는 경우 [응용 프로그램 패키지](batch-application-packages.md)도 요금이 청구 되므로 hello Azure 저장소 리소스에 대 한 응용 프로그램 패키지를 사용 하 합니다. 일반적으로 hello Azure 저장소 비용이 최소화 됩니다. 

## <a name="next-steps"></a>다음 단계
### <a name="batch-python-tutorial"></a>Batch Python 자습서
방법에 대 한 자세한 자습서에 대 한 Python, 체크 아웃을 사용 하 여 일괄 처리와 toowork [hello Azure 일괄 처리 Python 클라이언트 시작](batch-python-tutorial.md)합니다. 해당 도우미 [코드 샘플] [ github_samples_pyclient] 도우미 함수가 포함 되어 `get_vm_config_for_distro`, 다른 기술 tooobtain를 보여 주는 가상 컴퓨터 구성.

### <a name="batch-python-code-samples"></a>Batch Python 코드 샘플
hello [Python 코드 샘플] [ github_samples_py] hello에 [azure 일괄 처리-샘플] [ github_samples] 방법을 소개 하는 스크립트를 포함 하는 GitHub의 리포지토리 tooperform 일괄 처리와 같은 일반적인 작업이 풀, 작업 및 작업 만들기. hello [README] [ github_py_readme] hello Python 샘플을 포함 하는 방법을 tooinstall hello 필요한 패키지에 대 한 세부 정보를 포함 합니다.

### <a name="batch-forum"></a>Batch 포럼
hello [Azure 배치 포럼] [ forum] 는 좋은 toodiscuss 일괄 처리를 놓고 hello 서비스에 대 한 질문은 msdn 합니다. 유용한 "고정된" 게시물을 참조하고 Batch 솔루션을 빌드하는 동안 질문이 생기면 게시합니다.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
