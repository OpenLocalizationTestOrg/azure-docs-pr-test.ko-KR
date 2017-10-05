---
title: "독립 실행형 Azure Service Fabric 클러스터 설정 | Microsoft Docs"
description: "동일한 컴퓨터에서 실행되는 3개의 노드가 있는 독립 실행형 개발 클러스터를 만듭니다. 이 설정을 마치면 다중 컴퓨터 클러스터를 만들 수 있습니다."
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
ms.openlocfilehash: 5c8f4c784eed7b64810a3dd1c36c043d22a66936
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-standalone-cluster"></a><span data-ttu-id="02252-104">첫 번째 Service Fabric 독립 실행형 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="02252-104">Create your first Service Fabric standalone cluster</span></span>
<span data-ttu-id="02252-105">온-프레미스 또는 클라우드에 Windows Server 2012 R2 또는 Windows Server 2016을 실행하는 컴퓨터나 가상 컴퓨터에 Service Fabric 독립 실행형 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02252-105">You can create a Service Fabric standalone cluster on any virtual machines or computers running Windows Server 2012 R2 or Windows Server 2016, on-premises or in the cloud.</span></span> <span data-ttu-id="02252-106">이 빠른 시작을 통해 몇 분만에 독립 실행형 개발 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02252-106">This quickstart helps you to create a development standalone cluster in just a few minutes.</span></span>  <span data-ttu-id="02252-107">작업을 완료하면 앱을 배포할 수 있는 단일 컴퓨터에 3개 노드 클러스터가 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="02252-107">When you're finished, you have a three-node cluster running on a single computer that you can deploy apps to.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="02252-108">시작하기 전에</span><span class="sxs-lookup"><span data-stu-id="02252-108">Before you begin</span></span>
<span data-ttu-id="02252-109">Service Fabric은 독립 실행형 Service Fabric 클러스터를 만드는 설치 패키지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-109">Service Fabric provides a setup package to create Service Fabric standalone clusters.</span></span>  <span data-ttu-id="02252-110">[설치 패키지를 다운로드합니다](http://go.microsoft.com/fwlink/?LinkId=730690).</span><span class="sxs-lookup"><span data-stu-id="02252-110">[Download the setup package](http://go.microsoft.com/fwlink/?LinkId=730690).</span></span>  <span data-ttu-id="02252-111">개발 클러스터를 설정한 컴퓨터 또는 가상 컴퓨터의 폴더에 설치 패키지의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="02252-111">Unzip the setup package to a folder on the computer or virtual machine where you are setting up the development cluster.</span></span>  <span data-ttu-id="02252-112">설치 패키지의 내용은 [여기](service-fabric-cluster-standalone-package-contents.md)에서 자세히 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-112">The contents of the setup package are described in detail [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="02252-113">클러스터를 배포하고 구성하는 클러스터 관리자는 컴퓨터에서 관리자 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-113">The cluster administrator deploying and configuring the cluster must have administrator privileges on the computer.</span></span> <span data-ttu-id="02252-114">도메인 컨트롤러에 Service Fabric을 설치할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02252-114">You cannot install Service Fabric on a domain controller.</span></span>

## <a name="validate-the-environment"></a><span data-ttu-id="02252-115">환경 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="02252-115">Validate the environment</span></span>
<span data-ttu-id="02252-116">독립 실행형 패키지의 *TestConfiguration.ps1* 스크립트는 지정된 환경에 클러스터를 배포할 수 있는지 여부를 확인하는 모범 사례 분석기로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="02252-116">The *TestConfiguration.ps1* script in the standalone package is used as a best practices analyzer to validate whether a cluster can be deployed on a given environment.</span></span> <span data-ttu-id="02252-117">[배포 준비](service-fabric-cluster-standalone-deployment-preparation.md)는 필수 구성 요소 및 환경 요구 사항을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-117">[Deployment preparation](service-fabric-cluster-standalone-deployment-preparation.md) lists the pre-requisites and environment requirements.</span></span> <span data-ttu-id="02252-118">개발 클러스터를 만들 수 있는지 확인하는 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-118">Run the script to verify if you can create the development cluster:</span></span>

```powershell
.\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json
```
## <a name="create-the-cluster"></a><span data-ttu-id="02252-119">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="02252-119">Create the cluster</span></span>
<span data-ttu-id="02252-120">몇 가지 샘플 클러스터 구성 파일은 설치 패키지와 함께 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="02252-120">Several sample cluster configuration files are installed with the setup package.</span></span> <span data-ttu-id="02252-121">*ClusterConfig.Unsecure.DevCluster.json*은 가장 간단한 클러스터 구성: 단일 컴퓨터에서 실행되는 비보안 3개 노드 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="02252-121">*ClusterConfig.Unsecure.DevCluster.json* is the simplest cluster configuration: an unsecure, three-node cluster running on a single computer.</span></span>  <span data-ttu-id="02252-122">다른 구성 파일에서는 X.509 인증서 또는 Windows 보안을 사용하여 보호되는 단일 또는 다중 컴퓨터 클러스터를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-122">Other config files describe single or multi-machine clusters secured with X.509 certificates or Windows security.</span></span>  <span data-ttu-id="02252-123">이 자습서에 대한 기본 구성 설정을 수정할 필요는 없지만 구성 파일을 확인하고 설정에 익숙해지도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-123">You don't need to modify any of the default config settings for this tutorial, but look through the config file and get familiar with the settings.</span></span>  <span data-ttu-id="02252-124">**노드** 섹션에서는 클러스터에 있는 세 개의 노드(이름, IP 주소, [노드 유형, 장애 도메인 및 업그레이드 도메인](service-fabric-cluster-manifest.md#nodes-on-the-cluster))에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-124">The **nodes** section describes the three nodes in the cluster: name, IP address, [node type, fault domain, and upgrade domain](service-fabric-cluster-manifest.md#nodes-on-the-cluster).</span></span>  <span data-ttu-id="02252-125">**속성** 섹션에서는 클러스터의 [보안, 안정성 수준, 진단 컬렉션 수준 및 노드의 형식](service-fabric-cluster-manifest.md#cluster-properties)을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-125">The **properties** section defines the [security, reliability level, diagnostics collection, and types of nodes](service-fabric-cluster-manifest.md#cluster-properties) for the cluster.</span></span>

<span data-ttu-id="02252-126">이 클러스터는 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="02252-126">This cluster is unsecure.</span></span>  <span data-ttu-id="02252-127">누구든지 익명으로 연결하고 관리 작업을 수행할 수 있으므로 프로덕션 클러스터가 항상 X.509 인증서 또는 Windows 보안을 사용하여 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-127">Anyone can connect anonymously and perform management operations, so production clusters should always be secured using X.509 certificates or Windows security.</span></span>  <span data-ttu-id="02252-128">클러스터 생성 시에만 보안을 구성하므로 클러스터를 만든 후에 보안을 사용하도록 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="02252-128">Security is only configured at cluster creation time and it is not possible to enable security after the cluster is created.</span></span>  <span data-ttu-id="02252-129">Service Fabric 클러스터 보안에 대한 자세한 내용은 [클러스터에 보안 적용](service-fabric-cluster-security.md)을 읽어 보세요.</span><span class="sxs-lookup"><span data-stu-id="02252-129">Read [Secure a cluster](service-fabric-cluster-security.md) to learn more about Service Fabric cluster security.</span></span>  

<span data-ttu-id="02252-130">3개 노드 개발 클러스터를 만들려면 관리자 PowerShell 세션에서 *CreateServiceFabricCluster.ps1* 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-130">To create the three-node development cluster, run the *CreateServiceFabricCluster.ps1* script from an administrator PowerShell session:</span></span>

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="02252-131">Service Fabric 런타임 패키지는 클러스터 생성 시 자동으로 다운로드되어 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="02252-131">The Service Fabric runtime package is automatically downloaded and installed at time of cluster creation.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="02252-132">클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="02252-132">Connect to the cluster</span></span>
<span data-ttu-id="02252-133">3개 노드 개발 클러스터가 현재 실행 중입니다.</span><span class="sxs-lookup"><span data-stu-id="02252-133">Your three-node development cluster is now running.</span></span> <span data-ttu-id="02252-134">ServiceFabric PowerShell 모듈은 런타임에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="02252-134">The ServiceFabric PowerShell module is installed with the runtime.</span></span>  <span data-ttu-id="02252-135">Service Fabric 런타임에 클러스터가 같은 컴퓨터에서 실행되는지, 원격 컴퓨터에서 실행되는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02252-135">You can verify that the cluster is running from the same computer or from a remote computer with the Service Fabric runtime.</span></span>  <span data-ttu-id="02252-136">[Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet은 클러스터에 대한 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-136">The [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection to the cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint localhost:19000
```
<span data-ttu-id="02252-137">클러스터에 연결하는 다른 예제는 [보안 클러스터에 연결](service-fabric-connect-to-secure-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="02252-137">See [Connect to a secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting to a cluster.</span></span> <span data-ttu-id="02252-138">클러스터에 연결한 후에는 [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet을 사용하여 클러스터의 노드 목록과 각 노드에 대한 상태 정보를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-138">After connecting to the cluster, use the [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet to display a list of nodes in the cluster and status information for each node.</span></span> <span data-ttu-id="02252-139">**HealthState**는 노드마다 *OK* 상태여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-139">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- -------- --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     vm2      localhost       NodeType2 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm1      localhost       NodeType1 5.6.220.9494 0                     Up 00:03:38   00:00:00              OK
                     vm0      localhost       NodeType0 5.6.220.9494 0                     Up 00:02:43   00:00:00              OK
```

## <a name="visualize-the-cluster-using-service-fabric-explorer"></a><span data-ttu-id="02252-140">Service Fabric Explorer를 사용하여 클러스터 시각화</span><span class="sxs-lookup"><span data-stu-id="02252-140">Visualize the cluster using Service Fabric explorer</span></span>
<span data-ttu-id="02252-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md)는 클러스터를 시각화하고 응용 프로그램을 관리할 수 있는 좋은 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="02252-141">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="02252-142">Service Fabric Explorer는 브라우저를 사용하여 [http://localhost:19080/Explorer](http://localhost:19080/Explorer)로 이동하여 액세스할 수 있는 클러스터에서 실행되는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="02252-142">Service Fabric Explorer is a service that runs in the cluster, which you access using a browser by navigating to [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> 

<span data-ttu-id="02252-143">클러스터 대시보드는 응용 프로그램 및 노드 상태에 대한 요약을 포함하여 클러스터에 대한 개요를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-143">The cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="02252-144">노드 보기는 클러스터의 물리적 레이아웃을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="02252-144">The node view shows the physical layout of the cluster.</span></span> <span data-ttu-id="02252-145">지정된 노드의 경우 해당 노드에 배포된 코드를 가진 응용 프로그램을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02252-145">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

## <a name="remove-the-cluster"></a><span data-ttu-id="02252-147">클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="02252-147">Remove the cluster</span></span>
<span data-ttu-id="02252-148">클러스터를 제거하려면 패키지 폴더에서 *RemoveServiceFabricCluster.ps1* Powershell 스크립트를 실행하고 JSON 구성 파일에 대한 경로를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-148">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="02252-149">경우에 따라 삭제 로그 위치를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="02252-149">You can optionally specify a location for the log of the deletion.</span></span>

```powershell
# Removes Service Fabric cluster nodes from each computer in the configuration file.
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -Force
```

<span data-ttu-id="02252-150">컴퓨터에서 Service Fabric 런타임을 제거하려면 패키지 폴더에서 다음 PowerShell 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-150">To remove the Service Fabric runtime from the computer, run the following PowerShell script from the package folder.</span></span>

```powershell
# Removes Service Fabric from the current computer.
.\CleanFabric.ps1
```

## <a name="next-steps"></a><span data-ttu-id="02252-151">다음 단계</span><span class="sxs-lookup"><span data-stu-id="02252-151">Next steps</span></span>
<span data-ttu-id="02252-152">이제 독립 실행형 개발 클러스터를 설정했으며 다음 문서를 사용해보세요.</span><span class="sxs-lookup"><span data-stu-id="02252-152">Now that you have set up a development standalone cluster, try the following articles:</span></span>
* <span data-ttu-id="02252-153">[다중 컴퓨터 독립 실행형 클러스터를 설정](service-fabric-cluster-creation-for-windows-server.md)하고 보안을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="02252-153">[Set up a multi-machine standalone cluster](service-fabric-cluster-creation-for-windows-server.md) and enable security.</span></span>
* [<span data-ttu-id="02252-154">PowerShell을 사용하여 앱 배포</span><span class="sxs-lookup"><span data-stu-id="02252-154">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)

[service-fabric-explorer]: ./media/service-fabric-get-started-standalone-cluster/sfx.png
