---
title: "독립 실행형 Azure Service Fabric 클러스터 만들기 | Microsoft Docs"
description: "온-프레미스 또는 클라우드에서 Windows Server 컴퓨터(실제 또는 가상)를 사용하여 Azure Service Fabric 클러스터를 만듭니다."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 31349169-de19-4be6-8742-ca20ac41eb9e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/10/2017
ms.author: chackdan;maburlik;dekapur
ms.openlocfilehash: 6aa2905a97ec6b8c125f2ab9572a8e40bf525b27
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="028ab-103">Windows Server에서 실행되는 독립 실행형 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="028ab-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="028ab-104">Azure Service Fabric을 사용하면 Windows Server를 실행 중인 가상 컴퓨터 또는 컴퓨터에서 Service Fabric 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-104">You can use Azure Service Fabric to create Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="028ab-105">즉, 온-프레미스 또는 클라우드 공급자에 서로 연결된 일련의 Windows Server 컴퓨터가 있는 환경에서 Service Fabric 응용 프로그램을 배포하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="028ab-106">서비스 패브릭은 독립 실행형 Windows Server 패키지라는 서비스 패브릭 클러스터를 만들 수 있는 설치 패키지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-106">Service Fabric provides a setup package to create Service Fabric clusters called the standalone Windows Server package.</span></span>

<span data-ttu-id="028ab-107">이 문서에서는 Service Fabric 독립 실행형 클러스터를 만들기 위한 단계를 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-107">This article walks you through the steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="028ab-108">이 독립 실행형 Windows Server 패키지는 상업적으로 제공되며 프로덕션 배포에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="028ab-109">이 패키지는 "Preview"에 있는 새 Service Fabric 기능을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="028ab-110">"[이 패키지에 포함된 미리 보기 기능](#previewfeatures_anchor)"까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-110">Scroll down to "[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="028ab-111">미리 보기 기능 목록 섹션입니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-111">section for the list of the preview features.</span></span> <span data-ttu-id="028ab-112">현재 [EULA 사본을 다운로드](http://go.microsoft.com/fwlink/?LinkID=733084)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-112">You can [download a copy of the EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="028ab-113">Windows Server용 Service Fabric 패키지 지원</span><span class="sxs-lookup"><span data-stu-id="028ab-113">Get support for the Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="028ab-114">[Azure Service Fabric 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?)에서 Windows Server용 Service Fabric 독립 실행형 패키지에 대해 커뮤니티에 문의합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-114">Ask the community about the Service Fabric standalone package for Windows Server in the [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="028ab-115">[Service Fabric에 대한 전문 지원](http://support.microsoft.com/oas/default.aspx?prid=16146)에 대한 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="028ab-116">[여기](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0)에서 Microsoft의 전문 지원에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="028ab-117">또한 [Microsoft 프리미어 지원](https://support.microsoft.com/en-us/premier)의 일부로 이 패키지에 대해 지원을 받을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="028ab-118">자세한 내용은 [Azure Service Fabric 지원 옵션](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="028ab-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="028ab-119">지원을 위해 로그를 수집하려면 [Service Fabric 독립 실행형 로그 수집기](service-fabric-cluster-standalone-package-contents.md)를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-119">To collect logs for support purposes, run the [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-the-service-fabric-for-windows-server-package"></a><span data-ttu-id="028ab-120">Windows Server용 Service Fabric 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="028ab-120">Download the Service Fabric for Windows Server package</span></span>
<span data-ttu-id="028ab-121">클러스터를 만들려면 다음에서 찾을 수 있는 Windows Server(Windows Server 2012 R2 이상)용 Service Fabric 패키지를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-121">To create the cluster, use the Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="028ab-122">
[다운로드 링크 - Service Fabric 독립 실행형 패키지 - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="028ab-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="028ab-123">[여기](service-fabric-cluster-standalone-package-contents.md)에서 패키지의 자세한 내용을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-123">Find details on contents of the package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="028ab-124">Service Fabric 런타임 패키지는 클러스터 생성 시 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-124">The Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="028ab-125">인터넷에 연결되지 않은 컴퓨터에서 배포하는 경우 여기에서 대역 외 런타임 패키지를 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="028ab-125">If deploying from a machine not connected to the internet, please download the runtime package out of band from here:</span></span> <br><span data-ttu-id="028ab-126">
[다운로드 링크 - Service Fabric 런타임 - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="028ab-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="028ab-127">다음에서 독립 실행형 클러스터 구성 샘플을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="028ab-128">
[독립 실행형 클러스터 구성 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="028ab-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-the-cluster"></a><span data-ttu-id="028ab-129">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="028ab-129">Create the cluster</span></span>
<span data-ttu-id="028ab-130">[샘플](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)에 포함된 *ClusterConfig.Unsecure.DevCluster.json* 파일을 사용하여 하나의 컴퓨터 개발 클러스터에 Service Fabric을 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-130">Service Fabric can be deployed to a one-machine development cluster by using the *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="028ab-131">컴퓨터에 독립 실행형 패키지의 압축을 풀고 로컬 컴퓨터에 샘플 구성 파일을 복사한 다음 독립 실행형 패키지 폴더에서 관리자 PowerShell 세션을 통해 *CreateServiceFabricCluster.ps1* 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-131">Unpack the standalone package to your machine, copy the sample config file to the local machine, then run the *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from the standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="028ab-132">1A단계: 비보안 로컬 개발 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="028ab-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="028ab-133">문제 해결 세부 정보는 [클러스터 배포를 위한 계획 및 준비](service-fabric-cluster-standalone-deployment-preparation.md)에서 환경 설정 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="028ab-133">See the Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="028ab-134">실행 중인 개발 시나리오를 마친 경우 "[클러스터 제거](#removecluster_anchor)" 섹션의 단계를 참조하여 컴퓨터에서 Service Fabric 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-134">If you're finished running development scenarios, you can remove the Service Fabric cluster from the machine by referring to steps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="028ab-135">1B단계: 다중 컴퓨터 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="028ab-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="028ab-136">아래 링크에서 자세히 설명된 계획 및 준비 단계를 완료한 후 클러스터 구성 파일을 사용하여 프로덕션 클러스터를 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-136">After you have gone through the planning and preparation steps detailed at the below link, you are ready to create your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="028ab-137">
[클러스터 배포를 위한 계획 및 준비](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="028ab-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="028ab-138">독립 실행형 패키지 폴더에서 *TestConfiguration.ps1* 스크립트를 실행하여 작성한 구성 파일의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-138">Validate the configuration file you have written by running the *TestConfiguration.ps1* script from the standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="028ab-139">아래와 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-139">You should see output like below.</span></span> <span data-ttu-id="028ab-140">아래쪽 필드 "Passed"가 "True"로 반환되는 경우 온전성 검사를 통과했고 클러스터는 입력 구성에 따라 배포 가능한 것으로 보입니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-140">If the bottom field "Passed" is returned as "True", sanity checks have passed and the cluster looks to be deployable based on the input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written to existing trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
    Running Best Practices Analyzer...
    Best Practices Analyzer completed successfully.
    
    LocalAdminPrivilege        : True
    IsJsonValid                : True
    IsCabValid                 : True
    RequiredPortsOpen          : True
    RemoteRegistryAvailable    : True
    FirewallAvailable          : True
    RpcCheckPassed             : True
    NoConflictingInstallations : True
    FabricInstallable          : True
    Passed                     : True
    ```

2. <span data-ttu-id="028ab-141">클러스터 만들기: *CreateServiceFabricCluster.ps1* 스크립트를 실행하여 구성의 각 컴퓨터에 Service Fabric 클러스터를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-141">Create the cluster:  Run the *CreateServiceFabricCluster.ps1* script to deploy the Service Fabric cluster across each machine in the configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="028ab-142">CreateServiceFabricCluster.ps1 PowerShell 스크립트를 실행한 VM/컴퓨터에 배포 추적이 기록됩니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-142">Deployment traces are written to the VM/machine on which you ran the CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="028ab-143">스크립트가 실행된 디렉터리에 따라 하위 폴더 DeploymentTraces에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-143">These can be found in the subfolder DeploymentTraces, based in the directory from which the script was run.</span></span> <span data-ttu-id="028ab-144">Service Fabric이 컴퓨터에 올바르게 배포되었는지 확인하려면 클러스터 구성 파일 FabricSettings 섹션에서 설명된 대로 FabricDataRoot 디렉터리에 설치된 파일을 찾습니다(기본적으로 c:\ProgramData\SF).</span><span class="sxs-lookup"><span data-stu-id="028ab-144">To see if Service Fabric was deployed correctly to a machine, find the installed files in the FabricDataRoot directory, as detailed in the cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="028ab-145">또한 작업 관리자에서 실행 중인 FabricHost.exe 및 Fabric.exe 프로세스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="028ab-146">1C단계: 오프라인(인터넷 끊김) 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="028ab-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="028ab-147">Service Fabric 런타임 패키지는 클러스터 생성 시 자동으로 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-147">The Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="028ab-148">클러스터를 인터넷에 연결되지 않은 컴퓨터에 배포할 때 Service Fabric 런타임 패키지를 별도로 다운로드하고 클러스터 생성 시 경로를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-148">When deploying a cluster to machines not connected to the internet, you will need to download the Service Fabric runtime package separately, and provide the path to it at cluster creation.</span></span>
<span data-ttu-id="028ab-149">런타임 패키지는 [다운로드 링크 - Service Fabric 런타임 - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)에서 인터넷에 연결된 다른 컴퓨터에서 개별적으로 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-149">The runtime package can be downloaded separately, from another machine connected to the internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="028ab-150">오프라인 클러스터를 배포하는 위치에 런타임 패키지를 복사하고 아래와 같이 포함된 `-FabricRuntimePackagePath` 매개 변수를 사용하여 `CreateServiceFabricCluster.ps1`을 실행하여 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-150">Copy the runtime package to where you are deploying the offline cluster from, and create the cluster by running `CreateServiceFabricCluster.ps1` with the `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="028ab-151">여기서 `.\ClusterConfig.json` 및 `.\MicrosoftAzureServiceFabric.cab`는 각각 클러스터 구성 및 런타임 .cab 파일에 대한 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are the paths to the cluster configuration and the runtime .cab file respectively.</span></span>


### <a name="step-2-connect-to-the-cluster"></a><span data-ttu-id="028ab-152">2단계: 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="028ab-152">Step 2: Connect to the cluster</span></span>
<span data-ttu-id="028ab-153">보안 클러스터에 연결하려면 [보안 클러스터에 대한 Service Fabric 연결](service-fabric-connect-to-secure-cluster.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="028ab-153">To connect to a secure cluster, see [Service fabric connect to secure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="028ab-154">비보안 클러스터에 연결하려면 다음 PowerShell 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-154">To connect to an unsecure cluster, run the following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="028ab-155">예제:</span><span class="sxs-lookup"><span data-stu-id="028ab-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="028ab-156">3단계: Service Fabric Explorer 표시</span><span class="sxs-lookup"><span data-stu-id="028ab-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="028ab-157">이제 http://localhost:19080/Explorer/index.html을 사용하여 컴퓨터 중 하나에서 직접 또는 http://<*IPAddressofaMachine*>:19080/Explorer/index.html을 사용하여 원격으로 Service Fabric Explorer를 사용하여 클러스터에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-157">Now you can connect to the cluster with Service Fabric Explorer either directly from one of the machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="028ab-158">노드 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="028ab-158">Add and remove nodes</span></span>
<span data-ttu-id="028ab-159">비즈니스 요구가 변경됨에 따라 독립 실행형 서비스 패브릭 클러스터에 노드를 추가 또는 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-159">You can add or remove nodes to your standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="028ab-160">자세한 단계는 [서비스 패브릭 독립 실행형 클러스터에 노드 추가 또는 제거](service-fabric-cluster-windows-server-add-remove-nodes.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="028ab-160">See [Add or Remove nodes to a Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="028ab-161">클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="028ab-161">Remove a cluster</span></span>
<span data-ttu-id="028ab-162">클러스터를 제거하려면 패키지 폴더에서 *RemoveServiceFabricCluster.ps1* Powershell 스크립트를 실행하고 JSON 구성 파일에 대한 경로를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-162">To remove a cluster, run the *RemoveServiceFabricCluster.ps1* PowerShell script from the package folder and pass in the path to the JSON configuration file.</span></span> <span data-ttu-id="028ab-163">경우에 따라 삭제 로그 위치를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-163">You can optionally specify a location for the log of the deletion.</span></span>

<span data-ttu-id="028ab-164">이 스크립트는 클러스터 구성 파일에서 노드로 나열된 모든 컴퓨터에 대한 관리자 액세스 권한이 있는 모든 컴퓨터에서 실행될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-164">This script can be run on any machine that has administrator access to all the machines that are listed as nodes in the cluster configuration file.</span></span> <span data-ttu-id="028ab-165">이 스크립트가 실행되는 컴퓨터가 클러스터의 일부일 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-165">The machine that this script is run on does not have to be part of the cluster.</span></span>

```
# Removes Service Fabric from each machine in the configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from the current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-to-opt-out-of-it"></a><span data-ttu-id="028ab-166">수집된 원격 분석 데이터 및 옵트아웃(opt out)</span><span class="sxs-lookup"><span data-stu-id="028ab-166">Telemetry data collected and how to opt out of it</span></span>
<span data-ttu-id="028ab-167">기본적으로 이 제품은 제품을 개선하기 위해 Service Fabric 사용 현황에 대한 원격 분석을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-167">As a default, the product collects telemetry on the Service Fabric usage to improve the product.</span></span> <span data-ttu-id="028ab-168">설치의 일부로 실행되는 모범 사례 분석기는 [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1)에 대한 연결을 확인하고 연결할 수 없는 경우 원격 분석을 옵트아웃하지 않으면 설치가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-168">The Best Practice Analyzer that runs as a part of the setup checks for connectivity to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="028ab-169">연결할 수 없는 경우 원격 분석을 옵트아웃하지 않으면 설치가 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-169">If it is not reachable, the setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="028ab-170">원격 분석 파이프라인은 하루에 한 번 다음 데이터를 [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1)에 업로드하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-170">The telemetry pipeline tries to upload the following data to [https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="028ab-171">최상의 업로드이며 클러스터 기능에는 영향이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-171">It is a best-effort upload and has no impact on the cluster functionality.</span></span> <span data-ttu-id="028ab-172">원격 분석은 장애 조치(Failover) 관리자 기본이 실행되는 노드에서만 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-172">The telemetry is only sent from the node that runs the failover manager primary.</span></span> <span data-ttu-id="028ab-173">다른 노드에서는 원격 분석이 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="028ab-174">원격 분석은 다음으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-174">The telemetry consists of the following:</span></span>

* <span data-ttu-id="028ab-175">서비스 수</span><span class="sxs-lookup"><span data-stu-id="028ab-175">Number of services</span></span>
* <span data-ttu-id="028ab-176">ServiceTypes 수</span><span class="sxs-lookup"><span data-stu-id="028ab-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="028ab-177">응용 프로그램 수</span><span class="sxs-lookup"><span data-stu-id="028ab-177">Number of Applications</span></span>
* <span data-ttu-id="028ab-178">ApplicationUpgrades 수</span><span class="sxs-lookup"><span data-stu-id="028ab-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="028ab-179">FailoverUnits 수</span><span class="sxs-lookup"><span data-stu-id="028ab-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="028ab-180">InBuildFailoverUnits 수</span><span class="sxs-lookup"><span data-stu-id="028ab-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="028ab-181">UnhealthyFailoverUnits 수</span><span class="sxs-lookup"><span data-stu-id="028ab-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="028ab-182">복제본 수</span><span class="sxs-lookup"><span data-stu-id="028ab-182">Number of Replicas</span></span>
* <span data-ttu-id="028ab-183">InBuildReplicas 수</span><span class="sxs-lookup"><span data-stu-id="028ab-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="028ab-184">StandByReplicas 수</span><span class="sxs-lookup"><span data-stu-id="028ab-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="028ab-185">OfflineReplicas 수</span><span class="sxs-lookup"><span data-stu-id="028ab-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="028ab-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="028ab-186">CommonQueueLength</span></span>
* <span data-ttu-id="028ab-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="028ab-187">QueryQueueLength</span></span>
* <span data-ttu-id="028ab-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="028ab-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="028ab-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="028ab-189">CommitQueueLength</span></span>
* <span data-ttu-id="028ab-190">노드 수</span><span class="sxs-lookup"><span data-stu-id="028ab-190">Number of Nodes</span></span>
* <span data-ttu-id="028ab-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="028ab-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="028ab-192">ClusterId: 각 클러스터에 대해 임의로 생성된 GUID</span><span class="sxs-lookup"><span data-stu-id="028ab-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="028ab-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="028ab-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="028ab-194">원격 분석을 업로드한 가상 컴퓨터 또는 컴퓨터의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="028ab-194">IP address of the virtual machine or machine from which the telemetry is uploaded</span></span>

<span data-ttu-id="028ab-195">원격 분석을 사용하지 않도록 설정하려면 클러스터 config: *enableTelemetry: false*의 *properties*에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-195">To disable telemetry, add the following to *properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="028ab-196">이 패키지에 포함된 미리 보기 기능</span><span class="sxs-lookup"><span data-stu-id="028ab-196">Preview features included in this package</span></span>
<span data-ttu-id="028ab-197">없음.</span><span class="sxs-lookup"><span data-stu-id="028ab-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="028ab-198">새로운 [GA 버전의 Windows Server용 독립 실행형 클러스터(버전 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/)로 시작하는 경우 수동 또는 자동으로 클러스터를 후속 릴리스로 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="028ab-198">Starting with the new [GA version of the standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster to future releases, manually or automatically.</span></span> <span data-ttu-id="028ab-199">자세한 내용은 [독립 실행형 Service Fabric 클러스터 버전 업그레이드](service-fabric-cluster-upgrade-windows-server.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="028ab-199">Refer to [Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="028ab-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="028ab-200">Next steps</span></span>
* [<span data-ttu-id="028ab-201">PowerShell을 사용하여 응용 프로그램 배포 및 제거</span><span class="sxs-lookup"><span data-stu-id="028ab-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="028ab-202">독립 실행형 Windows 클러스터에 대한 구성 설정</span><span class="sxs-lookup"><span data-stu-id="028ab-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="028ab-203">독립 실행형 서비스 패브릭 클러스터에 노드 추가 또는 제거</span><span class="sxs-lookup"><span data-stu-id="028ab-203">Add or remove nodes to a standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="028ab-204">독립 실행형 Service Fabric 클러스터 버전 업그레이드</span><span class="sxs-lookup"><span data-stu-id="028ab-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="028ab-205">Windows를 실행하는 Azure VM에서 독립 실행형 서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="028ab-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="028ab-206">Windows 보안을 사용하여 독립 실행형 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="028ab-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="028ab-207">X509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="028ab-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
