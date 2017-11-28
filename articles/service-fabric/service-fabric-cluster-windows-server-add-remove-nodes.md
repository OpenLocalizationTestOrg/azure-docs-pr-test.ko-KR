---
title: "aaaAdd / 제거를 노드 tooa 독립 실행형 서비스 패브릭 클러스터 | Microsoft Docs"
description: "Tooadd / 제거를 노드 tooan Azure 서비스 패브릭 클러스터 물리적 컴퓨터 또는 온-프레미스 될 수 있는 Windows Server를 실행 하는 가상 컴퓨터에서 또는 클라우드의 모든 방법에 대해 알아봅니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="e8413-103">추가 또는 Windows Server에서 실행 하는 노드 tooa 독립 실행형 서비스 패브릭 클러스터를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="e8413-104">구성한 후 [Windows Server 컴퓨터에 독립 실행형 서비스 패브릭 클러스터를 만든](service-fabric-cluster-creation-for-windows-server.md), 비즈니스 요구에 맞게 변경 될 수 있으며 tooadd 필요 하거나 tooyour 클러스터 노드 제거 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="e8413-105">이 문서에서는이 단계를 자세히 tooachieve 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="e8413-106">노드 추가/제거 기능은 로컬 개발 클러스터에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="e8413-107">Tooyour 클러스터 노드 추가</span><span class="sxs-lookup"><span data-stu-id="e8413-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="e8413-108">준비 hello VM/컴퓨터 tooadd tooyour 클러스터 hello에 언급 된 hello 단계를 수행 하 여 원하는 [준비 hello 클러스터 배포에 대 한 toomeet hello 필수 구성 요소 컴퓨터](service-fabric-cluster-creation-for-windows-server.md) 섹션</span><span class="sxs-lookup"><span data-stu-id="e8413-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="e8413-109">어떤 장애 도메인과 업그레이드 도메인 이동 tooadd이 VM/컴퓨터를 식별 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="e8413-110">Hello tooadd toohello 클러스터를 지정 하는 VM/컴퓨터에 원격 데스크톱 (RDP)</span><span class="sxs-lookup"><span data-stu-id="e8413-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="e8413-111">복사 또는 [Windows Server 용 서비스 패브릭 용 hello 독립 실행형 패키지를 다운로드](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/컴퓨터 고 hello 패키지 압축을 풀면</span><span class="sxs-lookup"><span data-stu-id="e8413-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="e8413-112">상승 된 권한으로 Powershell을 실행 하 고 hello 압축 푼된 패키지의 toohello 위치를 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="e8413-113">Hello 실행 *AddNode.ps1* hello 새 노드 tooadd를 설명 하는 hello 매개 변수를 사용 하 여 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="e8413-114">VM5 라는 새 노드를 추가 하는 hello 예제 아래 형식과 NodeType0 및 IP 주소, 182.17.34.52, UD1 및 fd: / dc1/r 0입니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="e8413-115">hello *ExistingClusterConnectionEndPoint* hello 기존 클러스터의 노드에 대 한 연결 끝점을 이미은의 hello IP 주소 수 *모든* hello 클러스터에서 노드.</span><span class="sxs-lookup"><span data-stu-id="e8413-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="e8413-116">Hello 스크립트 실행이 종료 되 면 hello를 실행 하 여 hello 새 노드를 추가한 경우 확인할 수 있습니다 [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e8413-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="e8413-117">hello 클러스터의 다른 노드에서 tooensure 일관성을 구성 업그레이드를 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="e8413-118">실행 [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget 최신 구성 파일을 hello 및 hello 새로 실행 계정을 추가할 노드 너무 "노드" 섹션.</span><span class="sxs-lookup"><span data-stu-id="e8413-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="e8413-119">에 반드시 tooalways hello 최신 클러스터 구성 tooredploy hello 사용 하 여 클러스터 해야 하는 hello 사례에서 사용할 수 있는 동일한 구성 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="e8413-120">실행 [시작 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="e8413-121">서비스 패브릭 탐색기에 hello 업그레이드의 hello 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="e8413-122">또한 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="e8413-123">GMSA를 사용 하 여 Windows 보안을 사용 하 여 노드 tooclusters 구성 추가</span><span class="sxs-lookup"><span data-stu-id="e8413-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="e8413-124">gMSA(그룹 관리 서비스 계정)로 구성된 클러스터의 경우(https://technet.microsoft.com/library/hh831782.aspx) 구성 업그레이드를 사용하여 새 노드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="e8413-125">실행 [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello 최신 구성 파일을 세부 정보를 추가 hello 기존 노드에 원하는 tooadd "노드" hello"섹션에 새 노드 hello에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="e8413-126">Hello 새 노드는 일부 확인의 hello 같은 관리 되는 계정 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="e8413-127">이 계정은 모든 컴퓨터에서 관리자여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="e8413-128">실행 [시작 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="e8413-129">서비스 패브릭 탐색기에 hello 업그레이드의 hello 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="e8413-130">또한 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="e8413-131">노드 형식 tooyour 클러스터를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="e8413-132">에 새 노드 형식 tooadd 정렬 "속성"에 "NodeTypes" 섹션에서 구성 tooinclude hello 새 노드 형식을 수정 하 고는 구성을 시작 사용 하 여 업그레이드 [시작 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="e8413-133">Hello 업그레이드가 완료 된 후에이 노드 형식에 새 노드 tooyour 클러스터를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="e8413-134">클러스터에서 노드 제거</span><span class="sxs-lookup"><span data-stu-id="e8413-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="e8413-135">구성 업그레이드가 hello 방식으로 다음에서 사용 하 여 클러스터에서 노드를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="e8413-136">실행 [Get ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello 최신 구성 파일 및 *제거* "노드" 섹션에서 hello 노드.</span><span class="sxs-lookup"><span data-stu-id="e8413-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="e8413-137">"NodesToBeRemoved" hello 추가 매개 변수 너무 "설정" 섹션 "FabricSettings" 섹션.</span><span class="sxs-lookup"><span data-stu-id="e8413-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="e8413-138">"value" hello toobe 제거 해야 하는 노드의 노드 이름의 쉼표로 구분 된 목록 이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="e8413-139">실행 [시작 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello 업그레이드 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="e8413-140">서비스 패브릭 탐색기에 hello 업그레이드의 hello 진행률을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="e8413-141">또한 [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="e8413-142">노드를 제거하여 여러 업그레이드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="e8413-143">로 표시 된 일부 노드 `IsSeedNode=”true”` 태그를 지정 하 고 hello 클러스터를 쿼리하여 확인할 수 있습니다를 사용 하 여 매니페스트 `Get-ServiceFabricClusterManifest`합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="e8413-144">이러한 노드 제거 hello 시드 노드는 이러한 시나리오에서 이동 toobe 이므로 다른 항목 보다 더 오래 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="e8413-145">hello 클러스터는 최소 3 주 노드 유형 노드를 유지 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="e8413-146">클러스터에서 노드 유형 제거</span><span class="sxs-lookup"><span data-stu-id="e8413-146">Remove node types from your cluster</span></span>
<span data-ttu-id="e8413-147">노드 유형이 제거 하기 전에 hello 노드 유형을 참조 하 고 모든 노드가 다시 확인 하십시오.</span><span class="sxs-lookup"><span data-stu-id="e8413-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="e8413-148">Hello 해당 노드 형식을 제거 하기 전에 이러한 노드를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="e8413-149">Hello NodeType hello 클러스터 구성에서 제거 하 고는 구성을 시작 모든 해당 노드가 제거 되 면 사용 하 여 업그레이드 [시작 ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps)합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="e8413-150">클러스터의 주 노드 교체</span><span class="sxs-lookup"><span data-stu-id="e8413-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="e8413-151">기본 노드의 hello 대체 제거한 후 일괄 처리에 추가 하는 대신 다른 노드 하나 수행된 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e8413-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e8413-152">다음 단계</span><span class="sxs-lookup"><span data-stu-id="e8413-152">Next steps</span></span>
* [<span data-ttu-id="e8413-153">독립 실행형 Windows 클러스터에 대한 구성 설정</span><span class="sxs-lookup"><span data-stu-id="e8413-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="e8413-154">X509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="e8413-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="e8413-155">Windows를 실행하는 Azure VM에서 독립 실행형 서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="e8413-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

