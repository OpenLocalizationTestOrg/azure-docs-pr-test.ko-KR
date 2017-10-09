---
title: "독립 실행형 Azure 서비스 패브릭 클러스터를 aaaSet | Microsoft Docs"
description: "Hello에서 실행 되는 세 개의 노드가 있는 개발 독립 실행형 클러스터 만들기 같은 컴퓨터. 이 설치를 완료 한 후 준비 toocreate 다중 컴퓨터 클러스터 됩니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/06/2017
ms.author: dekapur
ms.openlocfilehash: e4d0ea9fc3b8475160bd8ed19fd3716463791cc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="256fa-104">첫 번째 Service Fabric 독립 실행형 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="256fa-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="256fa-105">Hello 클라우드 또는 가상 컴퓨터 또는 Windows Server 2012 R2 또는 Windows Server 2016에서 온-프레미스를 실행 하는 컴퓨터에 독립 실행형 서비스 패브릭 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in hello cloud.</span></span> <span data-ttu-id="256fa-106">이 빠른 시작 사용 하면 개발 독립 실행형 클러스터 toocreate 몇 분만에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-106">This quickstart helps you toocreate a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="256fa-107">작업을 완료하면 앱을 배포할 수 있는 단일 컴퓨터에 3개 노드 클러스터가 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="256fa-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="256fa-108">Before you begin</span></span>
<span data-ttu-id="256fa-109">서비스 패브릭 패키지 toocreate 서비스 패브릭 독립 실행형 클러스터 설치를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-109">Service Fabric provides a setup package toocreate Service Fabric standalone clusters.</span></span>  <span data-ttu-id="256fa-110">[Hello 설치 패키지를 다운로드](http://go.microsoft.com/fwlink/?LinkId=730690)합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-110">[Download hello setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="256fa-111">Hello 설치 패키지 tooa 폴더를에 hello 컴퓨터 또는 가상 컴퓨터를 설정 하는 hello 개발 클러스터 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-111">Unzip hello setup package tooa folder on hello computer or virtual machine where you are setting up hello development cluster.</span></span>  <span data-ttu-id="256fa-112">hello 설치 패키지의 hello 내용을 자세히 설명 되어 [여기](service-fabric-cluster-standalone-package-contents.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-112">hello contents of hello setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="256fa-113">클러스터 관리자에 게 배포 하 고 hello 클러스터 구성 hello 컴퓨터에서 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-113">hello cluster administrator deploying and configuring hello cluster must have administrator privileges on hello computer.</span></span> <span data-ttu-id="256fa-114">도메인 컨트롤러에 Service Fabric을 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-hello-environment"></a><span data-ttu-id="256fa-115">Hello 환경 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="256fa-115">Validate hello environment</span></span>
<span data-ttu-id="256fa-116">hello *TestConfiguration.ps1* hello 독립 실행형 패키지의 스크립트는 지정된 된 환경에는 클러스터를 배포할 수 있는지 여부를 모범 사례 분석기 toovalidate로 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-116">hello *TestConfiguration.ps1* script in hello standalone package is used as a best practices analyzer toovalidate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="256fa-117">[배포 준비](service-fabric-cluster-standalone-deployment-preparation.md) 목록 hello 필수 구성 요소 및 환경 요구 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists hello pre-requisites and environment requirements.</span></span> <span data-ttu-id="256fa-118">Hello 개발 클러스터를 만들 수 있으면 hello 스크립트 tooverify를 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-118">Run hello script tooverify if you can create hello development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-hello-cluster"></a><span data-ttu-id="256fa-119">Hello 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="256fa-119">Create hello cluster</span></span>
<span data-ttu-id="256fa-120">몇 가지 샘플 클러스터 구성 파일은 hello 설치 패키지와 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-120">Several sample cluster configuration files are installed with hello setup package.</span></span> <span data-ttu-id="256fa-121">*ClusterConfig.Unsecure.DevCluster.json* 는 hello 단순한 클러스터 구성: 단일 컴퓨터에서 실행 하는 보안 되지 않은, 3 개 노드 클러스터 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-121">*ClusterConfig.Unsecure.DevCluster.json* is hello simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="256fa-122">다른 구성 파일에서는 X.509 인증서 또는 Windows 보안을 사용하여 보호되는 단일 또는 다중 컴퓨터 클러스터를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="256fa-123">없습니다이 자습서에 대 한 기본 구성 설정을 hello toomodify를 필요 하지만 hello 구성 파일 전체를 검사 하 고 hello 설정에 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="256fa-123">You don't need toomodify any of hello default config settings for this tutorial, but look through hello config file and get familiar with hello settings.</span></span>  <span data-ttu-id="256fa-124">hello **노드** 설명 hello 클러스터에 세 개의 노드 hello: 이름, IP 주소 [노드 유형, 오류 도메인 및 업그레이드 도메인](service-fabric-cluster-manifest.md#nodes-on-the-cluster)합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-124">hello **nodes** section describes hello three nodes in hello cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="256fa-125">hello **속성** 섹션 정의 hello [보안, 신뢰성 수준, 진단 정보를 수집 및 유형의 노드](service-fabric-cluster-manifest.md#cluster-properties) hello 클러스터에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-125">hello **properties** section defines hello [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for hello cluster.</span></span>

<span data-ttu-id="256fa-126">이 클러스터는 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-126">This cluster is unsecure.</span></span>  <span data-ttu-id="256fa-127">누구든지 익명으로 연결하고 관리 작업을 수행할 수 있으므로 프로덕션 클러스터가 항상 X.509 인증서 또는 Windows 보안을 사용하여 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="256fa-128">보안 클러스터를 만들 때에만 구성 하 고 hello 클러스터가 만들어진 후 가능한 tooenable 보안은 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-128">Security is only configured at cluster creation time and it is not possible tooenable security after hello cluster is created.</span></span>  <span data-ttu-id="256fa-129">읽기 [클러스터 Secure](service-fabric-cluster-security.md) toolearn 서비스 패브릭 클러스터 보안에 대 한 자세한 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-129">Read [Secure a cluster](service-fabric-cluster-security.md) toolearn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="256fa-130">hello 실행 toocreate hello 3 노드 개발 클러스터 *CreateServiceFabricCluster.ps1* 관리자 PowerShell 세션에서 스크립트:</span><span class="sxs-lookup"><span data-stu-id="256fa-130">toocreate hello three-node development cluster, run hello *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="256fa-131">hello 서비스 패브릭 런타임 패키지가 자동으로 다운로드 하 클러스터를 만드는 시점에 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-131">hello Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="256fa-132">Toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="256fa-132">Connect toohello cluster</span></span>
<span data-ttu-id="256fa-133">3개 노드 개발 클러스터가 현재 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="256fa-134">hello ServiceFabric PowerShell 모듈 hello 런타임 함께 설치 됩니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-134">hello ServiceFabric PowerShell module is installed with hello runtime.</span></span>  <span data-ttu-id="256fa-135">해당 hello 클러스터가 hello에서 실행 중인지 확인할 수 있습니다 동일한 컴퓨터 또는 원격 컴퓨터 hello 서비스 패브릭 런타임 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-135">You can verify that hello cluster is running from hello same computer or from a remote computer with hello Service Fabric runtime.</span></span>  <span data-ttu-id="256fa-136">hello [Connect-servicefabriccluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet은 연결 toohello 클러스터를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-136">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="256fa-137">참조 [연결 tooa 보안 클러스터](service-fabric-connect-to-secure-cluster.md) 연결 tooa 클러스터의 다른 예입니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-137">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="256fa-138">연결 toohello 클러스터 후 hello를 사용 하 여 [Get ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay hello 클러스터 및 상태 정보를 각 노드에 대 한 노드 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-138">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="256fa-139">**HealthState**는 노드마다 *OK* 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="256fa-140">서비스 패브릭 탐색기를 사용 하 여 hello 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="256fa-140">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="256fa-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)는 클러스터를 시각화하고 응용 프로그램을 관리할 수 있는 좋은 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="256fa-142">서비스 패브릭 탐색기는 너무 이동 하 여 브라우저를 사용 하 여 액세스 하는 hello 클러스터에서 실행 되는 서비스[http://localhost:19080/탐색기](http://localhost:19080/Explorer)합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-142">Service Fabric Explorer is a service that runs in hello cluster, which you access using a browser by navigating too[http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="256fa-143">hello 클러스터 대시보드는 응용 프로그램 및 노드 상태 요약을 포함 하 여 클러스터에 대 한 개요를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-143">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="256fa-144">hello 노드 보기 hello hello 클러스터의 실제 레이아웃을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-144">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="256fa-145">지정된 노드의 경우 해당 노드에 배포된 코드를 가진 응용 프로그램을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-hello-cluster"></a><span data-ttu-id="256fa-147">Hello 클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="256fa-147">Remove hello cluster</span></span>
<span data-ttu-id="256fa-148">tooremove 클러스터 hello 실행 *RemoveServiceFabricCluster.ps1* hello 패키지 폴더와 hello 경로 toohello JSON 구성 파일의 단계에서 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-148">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="256fa-149">필요에 따라 hello 삭제의 hello 로그에 대 한 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-149">You can optionally specify a location for hello log of hello deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in hello configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="256fa-150">hello 패키지 폴더에서 PowerShell 스크립트 뒤 hello를 실행 하는 hello 컴퓨터에서 tooremove hello 서비스 패브릭 런타임입니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-150">tooremove hello Service Fabric runtime from hello computer, run hello following PowerShell script from hello package folder.</span></span>

```powershell
# Removes Service Fabric from hello current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="256fa-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="256fa-151">Next steps</span></span>
<span data-ttu-id="256fa-152">를 개발 독립 실행형 클러스터를 설정 하 hello 문서 다음을 시도해 보십시오.</span><span class="sxs-lookup"><span data-stu-id="256fa-152">Now that you have set up a development standalone cluster, try hello following articles:</span></span>
* <span data-ttu-id="256fa-153">[다중 컴퓨터 독립 실행형 클러스터를 설정](service-fabric-cluster-creation-for-windows-server.md)하고 보안을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="256fa-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="256fa-154">PowerShell을 사용하여 앱 배포</span><span class="sxs-lookup"><span data-stu-id="256fa-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
