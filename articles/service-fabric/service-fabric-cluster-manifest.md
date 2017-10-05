---
title: "Azure Service Fabric 독립 실행형 클러스터 구성 | Microsoft Docs"
description: "독립 실행형 또는 개인 Service Fabric 클러스터를 구성하는 방법에 대해 알아봅니다."
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
ms.openlocfilehash: 9885dce18dabac4a945dafd219e3ae190e34a83b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="configuration-settings-for-standalone-windows-cluster"></a><span data-ttu-id="637ee-103">독립 실행형 Windows 클러스터에 대한 구성 설정</span><span class="sxs-lookup"><span data-stu-id="637ee-103">Configuration settings for standalone Windows cluster</span></span>
<span data-ttu-id="637ee-104">이 문서에서는 ***ClusterConfig.JSON*** 파일을 사용하여 독립 실행형 Service Fabric 클러스터를 구성하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-104">This article describes how to configure a standalone Service Fabric cluster using the ***ClusterConfig.JSON*** file.</span></span> <span data-ttu-id="637ee-105">이 파일을 사용하여 독립 실행형 클러스터에 대한 Service Fabric 노드 및 해당 IP 주소, 클러스터의 다른 노드 형식, 보안 구성에 대한 정보와 장애/업그레이드 도메인과 관련된 네트워크 토폴로지에 대한 정보를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-105">You can use this file to specify information such as the Service Fabric nodes and their IP addresses, different types of nodes on the cluster, the security configurations as well as the network topology in terms of fault/upgrade domains, for your standalone cluster.</span></span>

<span data-ttu-id="637ee-106">[독립 실행형 Service Fabric 패키지를 다운로드](service-fabric-cluster-creation-for-windows-server.md#downloadpackage)하면 ClusterConfig.JSON 파일의 몇 가지 샘플이 작업 컴퓨터에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-106">When you [download the standalone Service Fabric package](service-fabric-cluster-creation-for-windows-server.md#downloadpackage), a few samples of the ClusterConfig.JSON file are downloaded to your work machine.</span></span> <span data-ttu-id="637ee-107">이름에 *DevCluster*가 있는 샘플은 논리 노드처럼 세 노드가 모두 동일한 컴퓨터에 있는 클러스터를 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-107">The samples having *DevCluster* in their names will help you create a cluster with all three nodes on the same machine, like logical nodes.</span></span> <span data-ttu-id="637ee-108">세 노드 중 하나 이상은 주 노드로 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-108">Out of these, at least one node must be marked as a primary node.</span></span> <span data-ttu-id="637ee-109">이 클러스터는 개발 또는 테스트 환경에 유용하며, 프로덕션 클러스터로 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-109">This cluster is useful for a development or test environment and is not supported as a production cluster.</span></span> <span data-ttu-id="637ee-110">이름에 *MultiMachine*이 있는 샘플은 각 노드가 별도의 컴퓨터에 있는 프로덕션 품질 클러스터를 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-110">The samples having *MultiMachine* in their names, will help you create a production quality cluster, with each node on a separate machine.</span></span>

1. <span data-ttu-id="637ee-111">*ClusterConfig.Unsecure.DevCluster.JSON* 및 *ClusterConfig.Unsecure.MultiMachine.JSON*은 각각 보안되지 않은 테스트 또는 프로덕션 클러스터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-111">*ClusterConfig.Unsecure.DevCluster.JSON* and *ClusterConfig.Unsecure.MultiMachine.JSON* show how to create an unsecured test or production cluster respectively.</span></span> 
2. <span data-ttu-id="637ee-112">*ClusterConfig.Windows.DevCluster.JSON* 및 *ClusterConfig.Windows.MultiMachine.JSON*은 [Windows 보안](service-fabric-windows-cluster-windows-security.md)을 사용하여 보안이 유지되는 테스트 또는 프로덕션 클러스터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-112">*ClusterConfig.Windows.DevCluster.JSON* and  *ClusterConfig.Windows.MultiMachine.JSON* show how to create test or production cluster, secured using [Windows security](service-fabric-windows-cluster-windows-security.md).</span></span>
3. <span data-ttu-id="637ee-113">*ClusterConfig.X509.DevCluster.JSON* 및 *ClusterConfig.X509.MultiMachine.JSON*은 [X509 인증서 기반 보안](service-fabric-windows-cluster-x509-security.md)을 사용하여 보안이 유지되는 테스트 또는 프로덕션 클러스터를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-113">*ClusterConfig.X509.DevCluster.JSON* and *ClusterConfig.X509.MultiMachine.JSON* show how to create test or production cluster, secured using [X509 certificate-based security](service-fabric-windows-cluster-x509-security.md).</span></span> 

<span data-ttu-id="637ee-114">이제 아래와 같이 ***ClusterConfig.JSON*** 파일의 여러 섹션을 검토해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-114">Now we will examine the various sections of a ***ClusterConfig.JSON*** file as below.</span></span>

## <a name="general-cluster-configurations"></a><span data-ttu-id="637ee-115">일반 클러스터 구성</span><span class="sxs-lookup"><span data-stu-id="637ee-115">General cluster configurations</span></span>
<span data-ttu-id="637ee-116">여기서는 아래의 JSON 코드 조각에 표시된 광범위한 클러스터별 구성을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-116">This covers the broad cluster specific configurations, as shown in the JSON snippet below.</span></span>

    "name": "SampleCluster",
    "clusterConfigurationVersion": "1.0.0",
    "apiVersion": "01-2017",

<span data-ttu-id="637ee-117">Service Fabric 클러스터를 **name** 변수에 할당하여 이름 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-117">You can give any friendly name to your Service Fabric cluster by assigning it to the **name** variable.</span></span> <span data-ttu-id="637ee-118">**clusterConfigurationVersion**은 클러스터의 버전 번호이며, Service Fabric 클러스터를 업그레이드할 때마다 증가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-118">The **clusterConfigurationVersion** is the version number of your cluster; you should increase it every time you upgrade your Service Fabric cluster.</span></span> <span data-ttu-id="637ee-119">그러나 **apiVersion**은 기본값으로 그대로 두어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-119">You should however leave the **apiVersion** to the default value.</span></span>

<a id="clusternodes"></a>

## <a name="nodes-on-the-cluster"></a><span data-ttu-id="637ee-120">클러스터의 노드</span><span class="sxs-lookup"><span data-stu-id="637ee-120">Nodes on the cluster</span></span>
<span data-ttu-id="637ee-121">다음 코드 조각처럼 **nodes** 섹션을 사용하여 Service Fabric 클러스터에서 노드를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-121">You can configure the nodes on your Service Fabric cluster by using the **nodes** section, as the following snippet shows.</span></span>

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

<span data-ttu-id="637ee-122">Service Fabric 클러스터에는 세 개 이상의 노드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-122">A Service Fabric cluster must contain at least 3 nodes.</span></span> <span data-ttu-id="637ee-123">설정에 따라 이 섹션에 노드를 더 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-123">You can add more nodes to this section as per your setup.</span></span> <span data-ttu-id="637ee-124">다음 표에서는 각 노드의 구성 설정에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-124">The following table explains the configuration settings for each node.</span></span>

| <span data-ttu-id="637ee-125">**노드 구성**</span><span class="sxs-lookup"><span data-stu-id="637ee-125">**Node configuration**</span></span> | <span data-ttu-id="637ee-126">**설명**</span><span class="sxs-lookup"><span data-stu-id="637ee-126">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="637ee-127">nodeName</span><span class="sxs-lookup"><span data-stu-id="637ee-127">nodeName</span></span> |<span data-ttu-id="637ee-128">노드에 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-128">You can give any friendly name to the node.</span></span> |
| <span data-ttu-id="637ee-129">iPAddress</span><span class="sxs-lookup"><span data-stu-id="637ee-129">iPAddress</span></span> |<span data-ttu-id="637ee-130">명령 창을 열고 `ipconfig`를 입력하여 노드의 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-130">Find out the IP address of your node by opening a command window and typing `ipconfig`.</span></span> <span data-ttu-id="637ee-131">IPV4 주소를 적어둔 후 **iPAddress** 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-131">Note the IPV4 address and assign it to the **iPAddress** variable.</span></span> |
| <span data-ttu-id="637ee-132">nodeTypeRef</span><span class="sxs-lookup"><span data-stu-id="637ee-132">nodeTypeRef</span></span> |<span data-ttu-id="637ee-133">노드마다 다른 노드 형식을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-133">Each node can be assigned a different node type.</span></span> <span data-ttu-id="637ee-134">[노드 형식](#nodetypes) 은 아래 섹션에 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-134">The [node types](#nodetypes) are defined in the section below.</span></span> |
| <span data-ttu-id="637ee-135">faultDomain</span><span class="sxs-lookup"><span data-stu-id="637ee-135">faultDomain</span></span> |<span data-ttu-id="637ee-136">장애 도메인은 클러스터 관리자가 공유되는 물리적 종속성으로 인해 동시에 장애를 경험할 가능성이 있는 실제 노드를 정의할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-136">Fault domains enable cluster administrators to define the physical nodes that might fail at the same time due to shared physical dependencies.</span></span> |
| <span data-ttu-id="637ee-137">upgradeDomain</span><span class="sxs-lookup"><span data-stu-id="637ee-137">upgradeDomain</span></span> |<span data-ttu-id="637ee-138">업그레이드 도메인은 Service Fabric 업그레이드를 위해 거의 같은 시간에 종료된 노드 집합을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-138">Upgrade domains describe sets of nodes that are shut down for Service Fabric upgrades at about the same time.</span></span> <span data-ttu-id="637ee-139">물리적 요구 사항에 따라 제한되지 않으므로 어떤 업그레이드 도메인에 어떤 노드를 할당할지 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-139">You can choose which nodes to assign to which Upgrade domains, as they are not limited by any physical requirements.</span></span> |

## <a name="cluster-properties"></a><span data-ttu-id="637ee-140">클러스터 속성</span><span class="sxs-lookup"><span data-stu-id="637ee-140">Cluster properties</span></span>
<span data-ttu-id="637ee-141">ClusterConfig.JSON의 **properties** 섹션은 다음과 같이 클러스터를 구성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-141">The **properties** section in the ClusterConfig.JSON is used to configure the cluster as follows.</span></span>

<a id="reliability"></a>

### <a name="reliability"></a><span data-ttu-id="637ee-142">안정성</span><span class="sxs-lookup"><span data-stu-id="637ee-142">Reliability</span></span>
<span data-ttu-id="637ee-143">**reliabilityLevel**이라는 개념은 클러스터의 주 노드에서 실행될 수 있는 Service Fabric 시스템 서비스의 복사본 또는 인스턴스 수를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-143">The concept of **reliabilityLevel** defines the number of replicas or instances of the Service Fabric system services that can run on the primary nodes of the cluster.</span></span> <span data-ttu-id="637ee-144">이는 이러한 서비스의 안정성 및 클러스터의 안정성을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-144">It determines the reliability of these services and hence the cluster.</span></span> <span data-ttu-id="637ee-145">값은 클러스터 생성 및 업그레이드 시 시스템에 의해 계산됩니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-145">The value is calcuated by the system at cluster creation and upgrade time.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="637ee-146">진단</span><span class="sxs-lookup"><span data-stu-id="637ee-146">Diagnostics</span></span>
<span data-ttu-id="637ee-147">다음 코드 조각과 같이 **diagnosticsStore** 섹션을 사용하여 진단 및 문제 해결 노드와 클러스터 오류를 사용하도록 매개 변수를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-147">The **diagnosticsStore** section allows you to configure parameters to enable diagnostics and troubleshooting node or cluster failures, as shown in the following snippet.</span></span> 

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "FileShare",
        "IsEncrypted": "false",
        "connectionstring": "c:\\ProgramData\\SF\\DiagnosticsStore"
    }

<span data-ttu-id="637ee-148">**metadata** 는 클러스터 진단에 대한 설명으로 설정에 따라 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-148">The **metadata** is a description of your cluster diagnostics and can be set as per your setup.</span></span> <span data-ttu-id="637ee-149">이러한 변수는 성능 카운터는 물론 ETW 추적 로그, 크래시 덤프를 수집하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-149">These variables help in collecting ETW trace logs, crash dumps as well as performance counters.</span></span> <span data-ttu-id="637ee-150">ETW 추적 로그에 대한 자세한 내용은 [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) 및 [ETW 추적](https://msdn.microsoft.com/library/ms751538.aspx)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="637ee-150">Read [Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx) and [ETW Tracing](https://msdn.microsoft.com/library/ms751538.aspx) for more information on ETW trace logs.</span></span> <span data-ttu-id="637ee-151">[크래시 덤프](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) 및 [성능 카운터](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx)를 포함하는 모든 로그는 컴퓨터의 **connectionString** 폴더로 보내질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-151">All logs including [Crash dumps](https://blogs.technet.microsoft.com/askperf/2008/01/08/understanding-crash-dump-files/) and [performance counters](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) can be directed to the **connectionString** folder on your machine.</span></span> <span data-ttu-id="637ee-152">진단을 저장하는 데 *AzureStorage* 를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-152">You can also use *AzureStorage* for storing diagnostics.</span></span> <span data-ttu-id="637ee-153">샘플 코드 조각에 대해서는 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="637ee-153">See below for a sample snippet.</span></span>

    "diagnosticsStore": {
        "metadata":  "Please replace the diagnostics store with an actual file share accessible from all cluster machines.",
        "dataDeletionAgeInDays": "7",
        "storeType": "AzureStorage",
        "IsEncrypted": "false",
        "connectionstring": "xstore:DefaultEndpointsProtocol=https;AccountName=[AzureAccountName];AccountKey=[AzureAccountKey]"
    }

### <a name="security"></a><span data-ttu-id="637ee-154">보안</span><span class="sxs-lookup"><span data-stu-id="637ee-154">Security</span></span>
<span data-ttu-id="637ee-155">**security** 섹션은 보안 독립 실행형 Service Fabric 클러스터에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-155">The **security** section is necessary for a secure standalone Service Fabric cluster.</span></span> <span data-ttu-id="637ee-156">다음 코드 조각에서는 이 섹션의 일부를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-156">The following snippet shows a part of this section.</span></span>

    "security": {
        "metadata": "This cluster is secured using X509 certificates.",
        "ClusterCredentialType": "X509",
        "ServerCredentialType": "X509",
        . . .
    }

<span data-ttu-id="637ee-157">**metadata** 는 보안 클러스터에 대한 설명으로 설정에 따라 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-157">The **metadata** is a description of your secure cluster and can be set as per your setup.</span></span> <span data-ttu-id="637ee-158">**ClusterCredentialType** 및 **ServerCredentialType**은 클러스터 및 노드가 구현하는 보안 유형을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-158">The **ClusterCredentialType** and **ServerCredentialType** determine the type of security that the cluster and the nodes will implement.</span></span> <span data-ttu-id="637ee-159">인증서 기반 보안의 경우는 *X509*로, Azure Active Directory 기반 보안의 경우는 *Windows*로 설정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-159">They can be set to either *X509* for a certificate-based security, or *Windows* for an Azure Active Directory-based security.</span></span> <span data-ttu-id="637ee-160">**security** 섹션의 나머지는 보안 유형을 기준으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-160">The rest of the **security** section will be based on the type of the security.</span></span> <span data-ttu-id="637ee-161">나머지 **security** 섹션을 채우는 방법에 대한 자세한 내용은 [독립 실행형 클러스터의 인증서 기반 보안](service-fabric-windows-cluster-x509-security.md) 또는 [독립 실행형 클러스터의 Windows 보안](service-fabric-windows-cluster-windows-security.md)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="637ee-161">Read [Certificates-based security in a standalone cluster](service-fabric-windows-cluster-x509-security.md) or [Windows security in a standalone cluster](service-fabric-windows-cluster-windows-security.md) for information on how to fill out the rest of the **security** section.</span></span>

<a id="nodetypes"></a>

### <a name="node-types"></a><span data-ttu-id="637ee-162">노드 형식</span><span class="sxs-lookup"><span data-stu-id="637ee-162">Node Types</span></span>
<span data-ttu-id="637ee-163">**nodeTypes** 섹션에서는 클러스터가 갖는 노드 형식에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-163">The **nodeTypes** section describes the type of the nodes that your cluster has.</span></span> <span data-ttu-id="637ee-164">아래 코드 조각처럼 클러스터에 대해 노드 형식을 하나 이상 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-164">At least one node type must be specified for a cluster, as shown in the snippet below.</span></span> 

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

<span data-ttu-id="637ee-165">**name** 은 이 특정 노드 형식의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-165">The **name** is the friendly name for this particular node type.</span></span> <span data-ttu-id="637ee-166">이 노드 형식의 노드를 만들려면 [위](#clusternodes)에 설명된 대로 해당 이름을 해당 노드의 **nodeTypeRef**에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-166">To create a node of this node type, assign its friendly name to the **nodeTypeRef** variable for that node, as mentioned [above](#clusternodes).</span></span> <span data-ttu-id="637ee-167">각 노드 형식에 대해 사용되는 연결 끝점을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-167">For each node type, define the connection endpoints that will be used.</span></span> <span data-ttu-id="637ee-168">이 클러스터의 다른 끝점과 충돌하지 않는 한, 이러한 연결 끝점에 대해 어떤 포트 번호도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-168">You can choose any port number for these connection endpoints, as long as they do not conflict with any other endpoints in this cluster.</span></span> <span data-ttu-id="637ee-169">다중 노드 클러스터에는 [**reliabilityLevel**](#reliability)에 따라 하나 이상의 주 노드가 있습니다(즉, **isPrimary**가 *true*로 설정됨).</span><span class="sxs-lookup"><span data-stu-id="637ee-169">In a multi-node cluster, there will be one or more primary nodes (i.e. **isPrimary** set to *true*), depending on the [**reliabilityLevel**](#reliability).</span></span> <span data-ttu-id="637ee-170">**nodeTypes** 및 **reliabilityLevel**에 대한 자세한 내용과 주 노드 형식 및 주 노드가 아닌 다른 노드 형식에 대한 자세한 내용은 [Service Fabric 클러스터 용량 계획 고려 사항](service-fabric-cluster-capacity.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="637ee-170">Read [Service Fabric cluster capacity planning considerations](service-fabric-cluster-capacity.md) for information on **nodeTypes** and **reliabilityLevel**, and to know what are primary and the non-primary node types.</span></span> 

#### <a name="endpoints-used-to-configure-the-node-types"></a><span data-ttu-id="637ee-171">노드 형식을 구성하는 데 사용되는 끝점</span><span class="sxs-lookup"><span data-stu-id="637ee-171">Endpoints used to configure the node types</span></span>
* <span data-ttu-id="637ee-172">*clientConnectionEndpointPort*는 클라이언트 API를 사용할 때 클라이언트에서 클러스터에 연결하는 데 사용되는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-172">*clientConnectionEndpointPort* is the port used by the client to connect to the cluster, when using the client APIs.</span></span> 
* <span data-ttu-id="637ee-173">*clusterConnectionEndpointPort*는 노드 간에 서로 통신하는 데 사용되는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-173">*clusterConnectionEndpointPort* is the port at which the nodes communicate with each other.</span></span>
* <span data-ttu-id="637ee-174">*leaseDriverEndpointPort*는 노드가 여전히 활성 상태인지 확인하기 위해 클러스터에서 드라이버를 임대하는 데 사용되는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-174">*leaseDriverEndpointPort* is the port used by the cluster lease driver to find out if the nodes are still active.</span></span> 
* <span data-ttu-id="637ee-175">*serviceConnectionEndpointPort*는 노드에 배포된 서비스 및 응용 프로그램에서 해당 특정 노드의 Service Fabric 클라이언트와 통신하는 데 사용되는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-175">*serviceConnectionEndpointPort* is the port used by the applications and services deployed on a node, to communicate with the Service Fabric client on that particular node.</span></span>
* <span data-ttu-id="637ee-176">*httpGatewayEndpointPort*는 Service Fabric Explorer에서 클러스터에 연결하는 데 사용되는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-176">*httpGatewayEndpointPort* is the port used by the Service Fabric Explorer to connect to the cluster.</span></span>
* <span data-ttu-id="637ee-177">*ephemeralPorts*는 [OS에서 사용되는 동적 포트](https://support.microsoft.com/kb/929851)를 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-177">*ephemeralPorts* override the [dynamic ports used by the OS](https://support.microsoft.com/kb/929851).</span></span> <span data-ttu-id="637ee-178">Service Fabric은 이 중 일부를 응용 프로그램 포트로 사용하고, 나머지를 OS에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-178">Service Fabric will use a part of these as application ports and the remaining will be available for the OS.</span></span> <span data-ttu-id="637ee-179">또한 이 범위를 OS에 있는 기존 범위에 매핑하므로 지정된 매핑을 JSON 파일에서 어떤 용도로든 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-179">It will also map this range to the existing range present in the OS, so for all purposes, you can use the ranges given in the sample JSON files.</span></span> <span data-ttu-id="637ee-180">시작 포트와 끝 포트 간의 차이가 255 이상인지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-180">You need to make sure that the difference between the start and the end ports is at least 255.</span></span> <span data-ttu-id="637ee-181">이 차이가 매우 낮으면 이 범위가 운영 체제에서 공유되므로 충돌이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-181">You may run into conflicts if this difference is too low, since this range is shared with the operating system.</span></span> <span data-ttu-id="637ee-182">`netsh int ipv4 show dynamicport tcp`를 실행하여 구성된 동적 포트 범위를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="637ee-182">See the configured dynamic port range by running `netsh int ipv4 show dynamicport tcp`.</span></span>
* <span data-ttu-id="637ee-183">*applicationPorts*는 Service Fabric 응용 프로그램에서 사용되는 포트입니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-183">*applicationPorts* are the ports that will be used by the Service Fabric applications.</span></span> <span data-ttu-id="637ee-184">응용 프로그램 포트 범위는 응용 프로그램의 끝점 요구 사항을 충족할 수 있을 만큼 충분히 커야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-184">The application port range should be large enough to cover the endpoint requirement of your applications.</span></span> <span data-ttu-id="637ee-185">이 범위는 컴퓨터의 동적 포트 범위, 즉 구성에 설정된 대로 *ephemeralPorts* 범위에서 제외되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-185">This range should be exclusive from the dynamic port range on the machine, i.e. the *ephemeralPorts* range as set in the configuration.</span></span>  <span data-ttu-id="637ee-186">Service Fabric은 새 포트가 필요할 때마다 이를 사용하며 이러한 포트의 방화벽 열기를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-186">Service Fabric will use these whenever new ports are required, as well as take care of opening the firewall for these ports.</span></span> 
* <span data-ttu-id="637ee-187">*reverseProxyEndpointPort*는 선택적 역방향 프록시 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-187">*reverseProxyEndpointPort* is an optional reverse proxy endpoint.</span></span> <span data-ttu-id="637ee-188">자세한 내용은 [Service Fabric 역방향 프록시](service-fabric-reverseproxy.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="637ee-188">See [Service Fabric Reverse Proxy](service-fabric-reverseproxy.md) for more details.</span></span> 

### <a name="log-settings"></a><span data-ttu-id="637ee-189">로그 설정</span><span class="sxs-lookup"><span data-stu-id="637ee-189">Log Settings</span></span>
<span data-ttu-id="637ee-190">**fabricSettings** 섹션에서는 Service Fabric 데이터 및 로그에 대한 루트 디렉터리를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-190">The **fabricSettings** section allows you to set the root directories for the Service Fabric data and logs.</span></span> <span data-ttu-id="637ee-191">이러한 디렉터리는 초기 클러스터 생성 중에만 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-191">You can customize these only during the initial cluster creation.</span></span> <span data-ttu-id="637ee-192">이 섹션의 샘플 코드 조각에 대해서는 아래를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="637ee-192">See below for a sample snippet of this section.</span></span>

    "fabricSettings": [{
        "name": "Setup",
        "parameters": [{
            "name": "FabricDataRoot",
            "value": "C:\\ProgramData\\SF"
        }, {
            "name": "FabricLogRoot",
            "value": "C:\\ProgramData\\SF\\Log"
    }]

<span data-ttu-id="637ee-193">OS가 아닌 드라이브를 사용하면 OS 충돌 시에도 더 큰 안정성을 제공하므로 이러한 드라이브를 FabricDataRoot 및 FabricLogRoot로 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-193">We recommended using a non-OS drive as the FabricDataRoot and FabricLogRoot as it provides more reliability against OS crashes.</span></span> <span data-ttu-id="637ee-194">데이터 루트만 사용자 지정하는 경우 로그 루트가 데이터 루트에서 한 수준 아래에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-194">Note that if you customize only the data root, then the log root will be placed one level below the data root.</span></span>

### <a name="stateful-reliable-service-settings"></a><span data-ttu-id="637ee-195">상태 저장 신뢰할 수 있는 서비스 설정</span><span class="sxs-lookup"><span data-stu-id="637ee-195">Stateful Reliable Service Settings</span></span>
<span data-ttu-id="637ee-196">**KtlLogger** 섹션에서는 Reliable Services에 대한 전역 구성 설정을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-196">The **KtlLogger** section allows you to set the global configuration settings for Reliable Services.</span></span> <span data-ttu-id="637ee-197">이러한 설정에 대한 자세한 내용 [상태 저장 신뢰할 수 있는 서비스 구성](service-fabric-reliable-services-configuration.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="637ee-197">For more details on these settings read [Configure stateful reliable services](service-fabric-reliable-services-configuration.md).</span></span>
<span data-ttu-id="637ee-198">아래 예제에서는 상태 저장 서비스에 대한 모든 신뢰할 수 있는 컬렉션 백업을 만드는 공유 트랜잭션 로그를 변경하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-198">The example below shows how to change the the shared transaction log that gets created to back any reliable collections for stateful services.</span></span>

    "fabricSettings": [{
        "name": "KtlLogger",
        "parameters": [{
            "name": "SharedLogSizeInMB",
            "value": "4096"
        }]
    }]

### <a name="add-on-features"></a><span data-ttu-id="637ee-199">추가 기능</span><span class="sxs-lookup"><span data-stu-id="637ee-199">Add-on features</span></span>
<span data-ttu-id="637ee-200">추가 기능을 구성하려면 apiVersion은 '04-2017' 이상으로 구성되어야 하며 addonFeatures를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-200">To configure add-on features, the apiVersion should be configured as '04-2017' or higher, and addonFeatures needs to be configured:</span></span>

    "apiVersion": "04-2017",
    "properties": {
      "addOnFeatures": [
          "DnsService",
          "RepairManager"
      ]
    }

### <a name="container-support"></a><span data-ttu-id="637ee-201">컨테이너 지원</span><span class="sxs-lookup"><span data-stu-id="637ee-201">Container support</span></span>
<span data-ttu-id="637ee-202">독립 실행형 클러스터에 대한 Windows Server 컨테이너와 hyper-v 컨테이너를 위한 컨테이너 지원을 사용하려면 'DnsService' 추가 기능을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-202">To enable container support for both windows server container and hyper-v container for standalone clusters, the 'DnsService' add-on feature needs to be enabled.</span></span>


## <a name="next-steps"></a><span data-ttu-id="637ee-203">다음 단계</span><span class="sxs-lookup"><span data-stu-id="637ee-203">Next steps</span></span>
<span data-ttu-id="637ee-204">독립 실행형 클러스터 설치에 따라 완전한 ClusterConfig.JSON 파일을 구성한 경우 [독립 실행형 Service Fabric 클러스터 만들기](service-fabric-cluster-creation-for-windows-server.md) 문서에 따라 클러스터를 배포한 다음 [Service Fabric Explorer로 클러스터 시각화](service-fabric-visualizing-your-cluster.md)를 계속 진행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="637ee-204">Once you have a complete ClusterConfig.JSON file configured as per your standalone cluster setup, you can deploy your cluster by following the article [Create a standalone Service Fabric cluster](service-fabric-cluster-creation-for-windows-server.md) and then proceed to [visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>

