---
title: "aaaConfigure 독립 실행형 Azure 서비스 패브릭 클러스터 | Microsoft Docs"
description: "자세한 내용은 방법 tooconfigure 독립 실행형 또는 개인 서비스 패브릭 클러스터입니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 0c5ec720-8f70-40bd-9f86-cd07b84a219d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/02/2017
ms.author: dekapur
ms.openlocfilehash: ce2ad387162a05668bbd3a271c754776fe471850
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="a0384-103">독립 실행형 Windows 클러스터에 대한 구성 설정</span><span class="sxs-lookup"><span data-stu-id="a0384-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="a0384-104">이 문서에서 설명 하는 방법을 사용 하 여 독립 실행형 서비스 패브릭 클러스터 tooconfigure hello ***ClusterConfig.JSON*** 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-104">This article describes how tooconfigure a standalone Service Fabric cluster using hello ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="a0384-105">독립 실행형 프로그램에 대 한 hello 네트워크 토폴로지 장애/업그레이드 도메인의 관점에서 뿐만 아니라 hello 클러스터, hello 보안 구성에이 파일 toospecify 정보 hello 서비스 패브릭 노드 및 해당 IP 주소, 다른 유형의 노드를 사용할 수 있습니다. 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-105">You can use this file toospecify information such as hello Service Fabric nodes and their IP addresses, different types of nodes on hello cluster, hello security configurations as well as hello network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="a0384-106">때 있습니다 [hello 독립 실행형 서비스 패브릭 패키지 다운로드](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), hello ClusterConfig.JSON 파일의 몇 가지 예제는 다운로드 한 tooyour 작업 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-106">When you [download hello standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of hello ClusterConfig.JSON file are downloaded tooyour work machine.</span></span> <span data-ttu-id="a0384-107">발생 하는 hello 샘플 *DevCluster* 이름에는 데 도움이 됩니다 hello 논리 노드 같이 동일한 컴퓨터에서 모든 세 개의 노드가 있는 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-107">hello samples having *DevCluster* in their names will help you create a cluster with all three nodes on hello same machine, like logical nodes.</span></span> <span data-ttu-id="a0384-108">세 노드 중 하나 이상은 주 노드로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="a0384-109">이 클러스터는 개발 또는 테스트 환경에 유용하며, 프로덕션 클러스터로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="a0384-110">발생 하는 hello 샘플 *MultiMachine* 이름에 만들 수 있습니다는 프로덕션 품질 클러스터 각 노드에 별도 컴퓨터.</span><span class="sxs-lookup"><span data-stu-id="a0384-110">hello samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="a0384-111">*ClusterConfig.Unsecure.DevCluster.JSON* 및 *ClusterConfig.Unsecure.MultiMachine.JSON* toocreate 안전 하지 않은 테스트 또는 프로덕션 각각 클러스터를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how toocreate an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="a0384-112">*ClusterConfig.Windows.DevCluster.JSON* 및 *ClusterConfig.Windows.MultiMachine.JSON* toocreate 테스트 또는 프로덕션 클러스터를 사용 하 여 보안 방법을 표시 [Windows 보안](service-fabric-windows-cluster-windows-security.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how toocreate test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="a0384-113">*ClusterConfig.X509.DevCluster.JSON* 및 *ClusterConfig.X509.MultiMachine.JSON* toocreate 테스트 또는 프로덕션 클러스터를 사용 하 여 보안 방법을 표시 [X509 인증서 기반 보안이](service-fabric-windows-cluster-x509-security.md).</span><span class="sxs-lookup"><span data-stu-id="a0384-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how toocreate test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="a0384-114">이제는 살펴보겠습니다 hello의 다양 한 섹션을 ***ClusterConfig.JSON*** 아래와 같이 파일.</span><span class="sxs-lookup"><span data-stu-id="a0384-114">Now we will examine hello various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="a0384-115">일반 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="a0384-115">General cluster configurations</span></span>
<span data-ttu-id="a0384-116">이 hello 광범위 한 클러스터 특정 구성 아래 hello JSON 조각에 표시 된 대로 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-116">This covers hello broad cluster specific configurations, as shown in hello JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="a0384-117">Toohello 할당 하 여 모든 이름을 tooyour 서비스 패브릭 클러스터를 제공할 수 있습니다 **이름** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-117">You can give any friendly name tooyour Service Fabric cluster by assigning it toohello **name** variable.</span></span> <span data-ttu-id="a0384-118">hello **clusterConfigurationVersion** ; 클러스터의 버전 번호 hello 서비스 패브릭 클러스터를 업그레이드할 때마다 증가 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-118">hello **clusterConfigurationVersion** is hello version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="a0384-119">그러나 유지 해야 합니다. hello **apiVersion** toohello 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-119">You should however leave hello **apiVersion** toohello default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-hello-cluster"></a><span data-ttu-id="a0384-120">Hello 클러스터의 노드</span><span class="sxs-lookup"><span data-stu-id="a0384-120">Nodes on hello cluster</span></span>
<span data-ttu-id="a0384-121">Hello를 사용 하 여 서비스 패브릭 클러스터에서 hello 노드를 구성할 수 있습니다 **노드** 조각과 다음 hello 처럼 섹션.</span><span class="sxs-lookup"><span data-stu-id="a0384-121">You can configure hello nodes on your Service Fabric cluster by using hello **nodes** section, as hello following snippet shows.</span></span>

    "nodes": [{
        "nodeName": "vm0",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType0",
        "faultDomain": "fd:/dc1/r0",
        "upgradeDomain": "UD0"
    }, {
        "nodeName": "vm1",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType1",
        "faultDomain": "fd:/dc1/r1",
        "upgradeDomain": "UD1"
    }, {
        "nodeName": "vm2",
        "iPAddress": "localhost",
        "nodeTypeRef": "NodeType2",
        "faultDomain": "fd:/dc1/r2",
        "upgradeDomain": "UD2"
    }],

<span data-ttu-id="a0384-122">Service Fabric 클러스터에는 세 개 이상의 노드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="a0384-123">설치 프로그램에 따라 더 많은 노드 toothis 섹션을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-123">You can add more nodes toothis section as per your setup.</span></span> <span data-ttu-id="a0384-124">다음 표에서 hello 각 노드에 대 한 hello 구성 설정에 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-124">hello following table explains hello configuration settings for each node.</span></span>

| <span data-ttu-id="a0384-125">**노드 구성**</span><span class="sxs-lookup"><span data-stu-id="a0384-125">**Node configuration**</span></span> | <span data-ttu-id="a0384-126">**설명**</span><span class="sxs-lookup"><span data-stu-id="a0384-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="a0384-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="a0384-127">nodeName</span></span> |<span data-ttu-id="a0384-128">식별 이름 toohello 노드를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-128">You can give any friendly name toohello node.</span></span> |
| <span data-ttu-id="a0384-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="a0384-129">iPAddress</span></span> |<span data-ttu-id="a0384-130">명령 창을 열고을 입력 하 여 노드의 hello IP 주소를 찾으려면 `ipconfig`합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-130">Find out hello IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="a0384-131">Hello IPV4 주소를 확인 하 고 toohello 할당 **iPAddress** 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-131">Note hello IPV4 address and assign it toohello **iPAddress** variable.</span></span> |
| <span data-ttu-id="a0384-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="a0384-132">nodeTypeRef</span></span> |<span data-ttu-id="a0384-133">노드마다 다른 노드 형식을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="a0384-134">hello [노드 형식](#nodetypes) hello 섹션 아래에 정의 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-134">hello [node types](#nodetypes) are defined in hello section below.</span></span> |
| <span data-ttu-id="a0384-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="a0384-135">faultDomain</span></span> |<span data-ttu-id="a0384-136">Tooshared 물리적 종속성 인해 시간이 오류 도메인 사용 되는 클러스터 관리자 toodefine hello 실제 노드 hello에 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-136">Fault domains enable cluster administrators toodefine hello physical nodes that might fail at hello same time due tooshared physical dependencies.</span></span> |
| <span data-ttu-id="a0384-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="a0384-137">upgradeDomain</span></span> |<span data-ttu-id="a0384-138">서비스 패브릭에 업그레이드 hello에 대 한 동일에 대 한 종료 된 노드 집합을 설명 하는 업그레이드 도메인 시간입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about hello same time.</span></span> <span data-ttu-id="a0384-139">모든 물리적 요구 사항에 따라 제한 되지 않습니다 대로 업그레이드 도메인 노드 tooassign toowhich를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-139">You can choose which nodes tooassign toowhich Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="a0384-140">클러스터 속성</span><span class="sxs-lookup"><span data-stu-id="a0384-140">Cluster properties</span></span>
<span data-ttu-id="a0384-141">hello **속성** 섹션 hello ClusterConfig.JSON에에서 사용 되는 tooconfigure hello 클러스터는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-141">hello **properties** section in hello ClusterConfig.JSON is used tooconfigure hello cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="a0384-142">안정성</span><span class="sxs-lookup"><span data-stu-id="a0384-142">Reliability</span></span>
<span data-ttu-id="a0384-143">hello 개념 **reliabilityLevel** 복제본 수가 hello 또는 hello 클러스터의 hello 주 노드에서 실행 될 수 있는 hello 서비스 패브릭 시스템 서비스의 인스턴스를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-143">hello concept of **reliabilityLevel** defines hello number of replicas or instances of hello Service Fabric system services that can run on hello primary nodes of hello cluster.</span></span> <span data-ttu-id="a0384-144">따라서 클러스터를 hello 및 이러한 서비스의 hello 안정성을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-144">It determines hello reliability of these services and hence hello cluster.</span></span> <span data-ttu-id="a0384-145">hello 기간은 hello 시스템에 의해 계산 된 클러스터 만들기 및 업그레이드 시입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-145">hello value is calcuated by hello system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="a0384-146">진단</span><span class="sxs-lookup"><span data-stu-id="a0384-146">Diagnostics</span></span>
<span data-ttu-id="a0384-147">hello **diagnosticsStore** 섹션 있습니다 tooconfigure 매개 변수 tooenable 진단 및 문제 해결 노드 또는 클러스터 오류 hello 다음 코드 조각에에서 나와 있는 것 처럼 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-147">hello **diagnosticsStore** section allows you tooconfigure parameters tooenable diagnostics and troubleshooting node or cluster failures, as shown in hello following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="a0384-148">hello **메타 데이터** 클러스터 진단에 대 한 설명을 이며 설치 프로그램에 따라 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-148">hello **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="a0384-149">이러한 변수는 성능 카운터는 물론 ETW 추적 로그, 크래시 덤프를 수집하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="a0384-150">ETW 추적 로그에 대한 자세한 내용은 [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) 및 [ETW 추적](https://msdn.microsoft.com/library/ms751538.aspx)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="a0384-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="a0384-151">포함 한 모든 로그 [크래시 덤프](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) 및 [÷ ´ ֹ](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) toohello 방향이 지정 된 수 **connectionString** 컴퓨터의 폴더에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed toohello **connectionString** folder on your machine.</span></span> <span data-ttu-id="a0384-152">진단을 저장하는 데 *AzureStorage* 를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="a0384-153">샘플 코드 조각에 대해서는 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0384-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace hello diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="a0384-154">보안</span><span class="sxs-lookup"><span data-stu-id="a0384-154">Security</span></span>
<span data-ttu-id="a0384-155">hello **보안** 섹션은 보안 독립 실행형 서비스 패브릭 클러스터에 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-155">hello **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="a0384-156">다음 코드 조각 hello이이 섹션의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-156">hello following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="a0384-157">hello **메타 데이터** 보안 클러스터에 대 한 설명을 이며 설치 프로그램에 따라 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-157">hello **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="a0384-158">hello **ClusterCredentialType** 및 **ServerCredentialType** hello hello 클러스터 및 hello 노드는 구현 하는 보안 형식을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-158">hello **ClusterCredentialType** and **ServerCredentialType** determine hello type of security that hello cluster and hello nodes will implement.</span></span> <span data-ttu-id="a0384-159">Tooeither를 설정할 수 있습니다 *X509* 인증서 기반 보안을 위해 또는 *Windows* Azure Active Directory 기반 보안에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-159">They can be set tooeither *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="a0384-160">hello 나머지 hello **보안** 섹션 hello 유형의 hello 보안에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-160">hello rest of hello **security** section will be based on hello type of hello security.</span></span> <span data-ttu-id="a0384-161">읽기 [독립 실행형 클러스터에서 인증서 기반 보안](service-fabric-windows-cluster-x509-security.md) 또는 [독립 실행형 클러스터에서 Windows 보안](service-fabric-windows-cluster-windows-security.md) hello 아웃 toofill hello 나머지 방법에 대 한 내용은 **보안**섹션.</span><span class="sxs-lookup"><span data-stu-id="a0384-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how toofill out hello rest of hello **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="a0384-162">노드 형식</span><span class="sxs-lookup"><span data-stu-id="a0384-162">Node Types</span></span>
<span data-ttu-id="a0384-163">hello **nodeTypes** 섹션에는 클러스터에 있는 hello 노드의 hello 유형에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-163">hello **nodeTypes** section describes hello type of hello nodes that your cluster has.</span></span> <span data-ttu-id="a0384-164">하나 이상의 노드 유형에 아래 hello 조각에 나와 있는 것 처럼 클러스터에 대해 지정 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-164">At least one node type must be specified for a cluster, as shown in hello snippet below.</span></span> 

    "nodeTypes": [{
        "name": "NodeType0",
        "clientConnectionEndpointPort": "19000",
        "clusterConnectionEndpointPort": "19001",
        "leaseDriverEndpointPort": "19002"
        "serviceConnectionEndpointPort": "19003",
        "httpGatewayEndpointPort": "19080",
        "reverseProxyEndpointPort": "19081",
        "applicationPorts": {
            "startPort": "20575",
            "endPort": "20605"
        },
        "ephemeralPorts": {
            "startPort": "20606",
            "endPort": "20861"
        },
        "isPrimary": true
    }]

<span data-ttu-id="a0384-165">hello **이름** 이 특정 노드 형식에 대 한 hello 친근 한 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-165">hello **name** is hello friendly name for this particular node type.</span></span> <span data-ttu-id="a0384-166">이 노드 유형의 노드 toocreate 할당의 식별 이름 toohello **nodeTypeRef** 설명 했 듯이 해당 노드에 대 한 변수 [위에](#clusternodes)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-166">toocreate a node of this node type, assign its friendly name toohello **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="a0384-167">각 노드 유형에 대해 사용 되는 hello 연결 끝점을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-167">For each node type, define hello connection endpoints that will be used.</span></span> <span data-ttu-id="a0384-168">이 클러스터의 다른 끝점과 충돌하지 않는 한, 이러한 연결 끝점에 대해 어떤 포트 번호도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="a0384-169">다중 노드 클러스터를 하나 이상의 주 노드가 됩니다 (즉, **isPrimary** 도*true*) hello에 따라 [ **reliabilityLevel** ](#reliability).</span><span class="sxs-lookup"><span data-stu-id="a0384-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set too*true*), depending on hello [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="a0384-170">읽기 [서비스 패브릭 클러스터 용량 계획 고려 사항](service-fabric-cluster-capacity.md) 에 대 한 내용은 **nodeTypes** 및 **reliabilityLevel**, 및는 주 대상과 hello tooknow 기본이 아닌 노드 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and tooknow what are primary and hello non-primary node types.</span></span> 

#### <a name="endpoints-used-tooconfigure-hello-node-types"></a><span data-ttu-id="a0384-171">끝점 사용 tooconfigure hello 노드 형식</span><span class="sxs-lookup"><span data-stu-id="a0384-171">Endpoints used tooconfigure hello node types</span></span>
* <span data-ttu-id="a0384-172">*clientConnectionEndpointPort* hello 클라이언트 Api를 사용 하는 경우 hello 클라이언트 tooconnect toohello 클러스터에서 사용 하는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-172">*clientConnectionEndpointPort* is hello port used by hello client tooconnect toohello cluster, when using hello client APIs.</span></span> 
* <span data-ttu-id="a0384-173">*clusterConnectionEndpointPort* hello 노드는 서로 통신 하는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-173">*clusterConnectionEndpointPort* is hello port at which hello nodes communicate with each other.</span></span>
* <span data-ttu-id="a0384-174">*leaseDriverEndpointPort* hello 노드가 아직 활성 상태인 경우 hello 아웃 임대 드라이버 toofind 클러스터에서 사용 하는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-174">*leaseDriverEndpointPort* is hello port used by hello cluster lease driver toofind out if hello nodes are still active.</span></span> 
* <span data-ttu-id="a0384-175">*serviceConnectionEndpointPort* 는 hello 응용 프로그램에서 사용 되는 hello 포트 및 서비스에 해당 특정 노드의 서비스 패브릭 클라이언트 hello와 toocommunicate 노드를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-175">*serviceConnectionEndpointPort* is hello port used by hello applications and services deployed on a node, toocommunicate with hello Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="a0384-176">*httpGatewayEndpointPort* hello 서비스 패브릭 탐색기 tooconnect toohello 클러스터에서 사용 하는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-176">*httpGatewayEndpointPort* is hello port used by hello Service Fabric Explorer tooconnect toohello cluster.</span></span>
* <span data-ttu-id="a0384-177">*ephemeralPorts* hello 재정의 [hello 운영 체제에서 사용 하는 동적 포트](https://support.microsoft.com/kb/929851)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-177">*ephemeralPorts* override hello [dynamic ports used by hello OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="a0384-178">서비스 패브릭 응용 프로그램 포트로 이러한 일부 ´ ֲ 및 hello 남은 hello OS에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-178">Service Fabric will use a part of these as application ports and hello remaining will be available for hello OS.</span></span> <span data-ttu-id="a0384-179">것도 매핑됩니다이 범위 toohello 기존 범위 hello OS에 있는 모든 용도 대 한 hello 샘플 JSON 파일에 지정 된 hello 범위를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-179">It will also map this range toohello existing range present in hello OS, so for all purposes, you can use hello ranges given in hello sample JSON files.</span></span> <span data-ttu-id="a0384-180">Toomake hello 차이 hello 시작 및 끝 포트 hello 이상 255 되는지 확인 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-180">You need toomake sure that hello difference between hello start and hello end ports is at least 255.</span></span> <span data-ttu-id="a0384-181">이러한 차이 hello 운영 체제와 공유 하는이 범위 때문에 너무 낮은 경우 충돌이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-181">You may run into conflicts if this difference is too low, since this range is shared with hello operating system.</span></span> <span data-ttu-id="a0384-182">실행 하 여 동적 포트 범위를 구성 하는 hello 참조 `netsh int ipv4 show dynamicport tcp`합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-182">See hello configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="a0384-183">*applicationPorts* 는 hello 서비스 패브릭 응용 프로그램에서 사용할 수는 hello 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-183">*applicationPorts* are hello ports that will be used by hello Service Fabric applications.</span></span> <span data-ttu-id="a0384-184">hello 응용 프로그램 포트 범위는 응용 프로그램의 hello 끝점 요구 사항을 충분히 큰 toocover 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-184">hello application port range should be large enough toocover hello endpoint requirement of your applications.</span></span> <span data-ttu-id="a0384-185">이 범위, 즉 hello hello 머신에서 hello 동적 포트 범위에서 배타적 해야 *ephemeralPorts* hello 구성에 설정 된 대로 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-185">This range should be exclusive from hello dynamic port range on hello machine, i.e. hello *ephemeralPorts* range as set in hello configuration.</span></span>  <span data-ttu-id="a0384-186">서비스 패브릭 새 포트 필요한으로 이러한 포트에 대 한 hello 방화벽을 열어 처리할 때마다이 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-186">Service Fabric will use these whenever new ports are required, as well as take care of opening hello firewall for these ports.</span></span> 
* <span data-ttu-id="a0384-187">*reverseProxyEndpointPort*는 선택적 역방향 프록시 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="a0384-188">자세한 내용은 [Service Fabric 역방향 프록시](service-fabric-reverseproxy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0384-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="a0384-189">로그 설정</span><span class="sxs-lookup"><span data-stu-id="a0384-189">Log Settings</span></span>
<span data-ttu-id="a0384-190">hello **fabricSettings** 섹션에서는 hello 서비스 패브릭 데이터와 로그에 대 한 tooset hello 루트 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-190">hello **fabricSettings** section allows you tooset hello root directories for hello Service Fabric data and logs.</span></span> <span data-ttu-id="a0384-191">Hello 초기 클러스터 생성 중에 이러한를 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-191">You can customize these only during hello initial cluster creation.</span></span> <span data-ttu-id="a0384-192">이 섹션의 샘플 코드 조각에 대해서는 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0384-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="a0384-193">및 사용 하 여 hello FabricDataRoot와 OS가 아닌 드라이브 FabricLogRoot OS 충돌에 대 한 안정성을 제공 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-193">We recommended using a non-OS drive as hello FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="a0384-194">Note만 hello 데이터 루트를 사용자 지정 하는 경우 다음 hello 로그 루트는 배치 하는 것 보다 한 수준 아래 hello 데이터 루트입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-194">Note that if you customize only hello data root, then hello log root will be placed one level below hello data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="a0384-195">상태 저장 신뢰할 수 있는 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="a0384-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="a0384-196">hello **KtlLogger** 섹션에서는 신뢰할 수 있는 서비스에 대 한 tooset hello 전역 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-196">hello **KtlLogger** section allows you tooset hello global configuration settings for Reliable Services.</span></span> <span data-ttu-id="a0384-197">이러한 설정에 대한 자세한 내용 [상태 저장 신뢰할 수 있는 서비스 구성](service-fabric-reliable-services-configuration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="a0384-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="a0384-198">다음 예제에서는 hello toochange hello hello 공유 트랜잭션 로그를 가져오는 만드는 방법을 tooback 상태 저장 서비스에 대 한 신뢰할 수 있는 모든 컬렉션 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-198">hello example below shows how toochange hello hello shared transaction log that gets created tooback any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="a0384-199">추가 기능</span><span class="sxs-lookup"><span data-stu-id="a0384-199">Add-on features</span></span>
<span data-ttu-id="a0384-200">tooconfigure 추가 기능 hello apiVersion 구성으로 ' 04-2017' 이상 이어야 합니다 하며 addonFeatures toobe 구성:</span><span class="sxs-lookup"><span data-stu-id="a0384-200">tooconfigure add-on features, hello apiVersion should be configured as '04-2017' or higher, and addonFeatures needs toobe configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="a0384-201">컨테이너 지원</span><span class="sxs-lookup"><span data-stu-id="a0384-201">Container support</span></span>
<span data-ttu-id="a0384-202">tooenable 컨테이너에 대 한 지원을 모두 windows server 컨테이너와 hyper-v 컨테이너 독립 실행형 클러스터에 대 한 hello 'DnsService' 부가 기능 toobe 사용 하도록 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-202">tooenable container support for both windows server container and hyper-v container for standalone clusters, hello 'DnsService' add-on feature needs toobe enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a0384-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="a0384-203">Next steps</span></span>
<span data-ttu-id="a0384-204">독립 실행형 클러스터 설치에 따라 구성 된 전체 ClusterConfig.JSON 파일을 만든 후 다음 hello 문서를 통해 클러스터를 배포할 수 있습니다 [독립 실행형 서비스 패브릭 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md) 너무 진행할[서비스 패브릭 탐색기를 사용 하 여 클러스터 시각화](service-fabric-visualizing-your-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="a0384-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following hello article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed too[visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

