---
title: "독립 실행형 Azure 서비스 패브릭 클러스터 aaaCreate | Microsoft Docs"
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
ms.openlocfilehash: 444970816290a0448d88a8b2082c75eb7a64cb44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-standalone-cluster-running-on-windows-server"></a><span data-ttu-id="646d5-103">Windows Server에서 실행되는 독립 실행형 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="646d5-103">Create a standalone cluster running on Windows Server</span></span>
<span data-ttu-id="646d5-104">모든 가상 컴퓨터 또는 Windows Server를 실행 하는 컴퓨터에 Azure 서비스 패브릭 toocreate 서비스 패브릭 클러스터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-104">You can use Azure Service Fabric toocreate Service Fabric clusters on any virtual machines or computers running Windows Server.</span></span> <span data-ttu-id="646d5-105">즉, 온-프레미스 또는 클라우드 공급자에 서로 연결된 일련의 Windows Server 컴퓨터가 있는 환경에서 Service Fabric 응용 프로그램을 배포하고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-105">This means you can deploy and run Service Fabric applications in any environment that contains a set of interconnected Windows Server computers, be it on premises or with any cloud provider.</span></span> <span data-ttu-id="646d5-106">서비스 패브릭 서비스 패브릭 클러스터 설치 패키지 toocreate 라는 hello 독립 실행형 Windows Server 패키지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-106">Service Fabric provides a setup package toocreate Service Fabric clusters called hello standalone Windows Server package.</span></span>

<span data-ttu-id="646d5-107">이 문서에서는 독립 실행형 서비스 패브릭 클러스터를 만들기 위한 hello 단계를 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-107">This article walks you through hello steps for creating a Service Fabric standalone cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="646d5-108">이 독립 실행형 Windows Server 패키지는 상업적으로 제공되며 프로덕션 배포에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-108">This standalone Windows Server package is commercially available and may be used for production deployments.</span></span> <span data-ttu-id="646d5-109">이 패키지는 "Preview"에 있는 새 Service Fabric 기능을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-109">This package may contain new Service Fabric features that are in "Preview".</span></span> <span data-ttu-id="646d5-110">너무 아래로 스크롤하여"[이 패키지에 포함 된 기능을 미리 볼](#previewfeatures_anchor)."</span><span class="sxs-lookup"><span data-stu-id="646d5-110">Scroll down too"[Preview features included in this package](#previewfeatures_anchor)."</span></span> <span data-ttu-id="646d5-111">섹션 hello 목록에 대 한 hello 미리 보기 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-111">section for hello list of hello preview features.</span></span> <span data-ttu-id="646d5-112">있습니다 수 [hello EULA 복사본을 다운로드](http://go.microsoft.com/fwlink/?LinkID=733084) 이제 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-112">You can [download a copy of hello EULA](http://go.microsoft.com/fwlink/?LinkID=733084) now.</span></span>
> 
> 

<a id="getsupport"></a>

## <a name="get-support-for-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="646d5-113">Windows Server 용 서비스 패브릭 패키지 hello에 대 한 지원 받기</span><span class="sxs-lookup"><span data-stu-id="646d5-113">Get support for hello Service Fabric for Windows Server package</span></span>
* <span data-ttu-id="646d5-114">Hello에 hello 서비스 패브릭 독립 실행형 패키지에 대해 Windows Server 용 hello 커뮤니티는 질문 [Azure 서비스 패브릭 포럼](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?)합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-114">Ask hello community about hello Service Fabric standalone package for Windows Server in hello [Azure Service Fabric forum](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=AzureServiceFabric?).</span></span>
* <span data-ttu-id="646d5-115">[Service Fabric에 대한 전문 지원](http://support.microsoft.com/oas/default.aspx?prid=16146)에 대한 티켓을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-115">Open a ticket for [Professional Support for Service Fabric](http://support.microsoft.com/oas/default.aspx?prid=16146).</span></span>  <span data-ttu-id="646d5-116">[여기](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0)에서 Microsoft의 전문 지원에 대해 자세히 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-116">Learn more about Professional Support from Microsoft [here](https://support.microsoft.com/en-us/gp/offerprophone?wa=wsignin1.0).</span></span>
* <span data-ttu-id="646d5-117">또한 [Microsoft 프리미어 지원](https://support.microsoft.com/en-us/premier)의 일부로 이 패키지에 대해 지원을 받을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-117">You can also get support for this package as a part of [Microsoft Premier Support](https://support.microsoft.com/en-us/premier).</span></span>
* <span data-ttu-id="646d5-118">자세한 내용은 [Azure Service Fabric 지원 옵션](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="646d5-118">For more details, please see [Azure Service Fabric support options](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-support).</span></span>
* <span data-ttu-id="646d5-119">hello 실행 지원을 위해 toocollect 로그 [서비스 패브릭 독립 실행형 로그 수집기](service-fabric-cluster-standalone-package-contents.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-119">toocollect logs for support purposes, run hello [Service Fabric Standalone Log collector](service-fabric-cluster-standalone-package-contents.md).</span></span>

<a id="downloadpackage"></a>

## <a name="download-hello-service-fabric-for-windows-server-package"></a><span data-ttu-id="646d5-120">Hello Windows Server 용 서비스 패브릭 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="646d5-120">Download hello Service Fabric for Windows Server package</span></span>
<span data-ttu-id="646d5-121">toocreate hello 클러스터를 사용 하 여 hello Windows Server 용 서비스 패브릭 패키지 (Windows Server 2012 R2 이상 버전) ´ ֿ ´:</span><span class="sxs-lookup"><span data-stu-id="646d5-121">toocreate hello cluster, use hello Service Fabric for Windows Server package (Windows Server 2012 R2 and newer) found here:</span></span> <br><span data-ttu-id="646d5-122">
[다운로드 링크 - Service Fabric 독립 실행형 패키지 - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span><span class="sxs-lookup"><span data-stu-id="646d5-122">
[Download Link - Service Fabric Standalone Package - Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690)</span></span>

<span data-ttu-id="646d5-123">Hello 패키지의 내용에 대 한 자세한 내용은 [여기](service-fabric-cluster-standalone-package-contents.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-123">Find details on contents of hello package [here](service-fabric-cluster-standalone-package-contents.md).</span></span>

<span data-ttu-id="646d5-124">hello 서비스 패브릭 런타임에서 패키지는 클러스터 생성 시 자동으로 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-124">hello Service Fabric runtime package is automatically downloaded at time of cluster creation.</span></span> <span data-ttu-id="646d5-125">Toohello 연결 되지 컴퓨터에서 배포 하는 경우 인터넷을 여기에서 out of band 방식 hello 런타임 패키지를 다운로드 하세요.</span><span class="sxs-lookup"><span data-stu-id="646d5-125">If deploying from a machine not connected toohello internet, please download hello runtime package out of band from here:</span></span> <br><span data-ttu-id="646d5-126">
[다운로드 링크 - Service Fabric 런타임 - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span><span class="sxs-lookup"><span data-stu-id="646d5-126">
[Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)</span></span>

<span data-ttu-id="646d5-127">다음에서 독립 실행형 클러스터 구성 샘플을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-127">Find Standalone Cluster Configuration samples at:</span></span> <br><span data-ttu-id="646d5-128">
[독립 실행형 클러스터 구성 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span><span class="sxs-lookup"><span data-stu-id="646d5-128">
[Standalone Cluster Configuration Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)</span></span>

<a id="createcluster"></a>

## <a name="create-hello-cluster"></a><span data-ttu-id="646d5-129">Hello 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="646d5-129">Create hello cluster</span></span>
<span data-ttu-id="646d5-130">서비스 패브릭 hello를 사용 하 여 배포 된 tooa 하나 컴퓨터 개발 클러스터 수 *ClusterConfig.Unsecure.DevCluster.json* 에 포함 된 파일 [샘플](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples)합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-130">Service Fabric can be deployed tooa one-machine development cluster by using hello *ClusterConfig.Unsecure.DevCluster.json* file included in [Samples](https://github.com/Azure-Samples/service-fabric-dotnet-standalone-cluster-configuration/tree/master/Samples).</span></span>

<span data-ttu-id="646d5-131">Hello 독립 실행형 패키지 tooyour 컴퓨터를 복사 hello 샘플 구성 파일 toohello 로컬 컴퓨터에서 다음 실행된 hello 압축 풀기 *CreateServiceFabricCluster.ps1* hello 독립 실행형에서 관리자 권한 PowerShell 세션을 통해 스크립트 패키지 폴더:</span><span class="sxs-lookup"><span data-stu-id="646d5-131">Unpack hello standalone package tooyour machine, copy hello sample config file toohello local machine, then run hello *CreateServiceFabricCluster.ps1* script through an administrator PowerShell session, from hello standalone package folder:</span></span>
### <a name="step-1a-create-an-unsecured-local-development-cluster"></a><span data-ttu-id="646d5-132">1A단계: 비보안 로컬 개발 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="646d5-132">Step 1A: Create an unsecured local development cluster</span></span>
```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.Unsecure.DevCluster.json -AcceptEULA
```

<span data-ttu-id="646d5-133">참조에서 환경 설정 섹션 hello [계획 하 고 클러스터 배포를 준비](service-fabric-cluster-standalone-deployment-preparation.md) 문제 해결 세부 정보에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-133">See hello Environment Setup section at [Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md) for troubleshooting details.</span></span>

<span data-ttu-id="646d5-134">실행 중인 개발 시나리오를 완료 하는 경우에서 제거할 수 있습니다 hello 서비스 패브릭 클러스터 hello 컴퓨터 toosteps 섹션에서 참조 하 여 "[클러스터 제거](#removecluster_anchor)"입니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-134">If you're finished running development scenarios, you can remove hello Service Fabric cluster from hello machine by referring toosteps in section "[Remove a cluster](#removecluster_anchor)".</span></span> 

### <a name="step-1b-create-a-multi-machine-cluster"></a><span data-ttu-id="646d5-135">1B단계: 다중 컴퓨터 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="646d5-135">Step 1B: Create a multi-machine cluster</span></span>
<span data-ttu-id="646d5-136">후에 hello 계획을 통해 모두 수행한 준비 단계에서 hello 링크를 아래에서 자세히 toocreate 클러스터 구성 파일을 사용 하 여 프로덕션 클러스터를 준비 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-136">After you have gone through hello planning and preparation steps detailed at hello below link, you are ready toocreate your production cluster using your cluster configuration file.</span></span> <br><span data-ttu-id="646d5-137">
[클러스터 배포를 위한 계획 및 준비](service-fabric-cluster-standalone-deployment-preparation.md)</span><span class="sxs-lookup"><span data-stu-id="646d5-137">
[Plan and prepare your cluster deployment](service-fabric-cluster-standalone-deployment-preparation.md)</span></span>

1. <span data-ttu-id="646d5-138">Hello를 실행 하 여 작성 한 hello 구성 파일의 유효성을 검사 *TestConfiguration.ps1* hello 독립 실행형 패키지 폴더에서 스크립트:</span><span class="sxs-lookup"><span data-stu-id="646d5-138">Validate hello configuration file you have written by running hello *TestConfiguration.ps1* script from hello standalone package folder:</span></span>  

    ```powershell
    .\TestConfiguration.ps1 -ClusterConfigFilePath .\ClusterConfig.json
    ```

    <span data-ttu-id="646d5-139">아래와 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-139">You should see output like below.</span></span> <span data-ttu-id="646d5-140">Hello 아래쪽 필드 "성공"이 "True"로 반환 되 면 온전성 검사에 통과 했음을 하 고 hello 클러스터 toobe 배포 가능한 hello 입력된 구성에 따라을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-140">If hello bottom field "Passed" is returned as "True", sanity checks have passed and hello cluster looks toobe deployable based on hello input configuration.</span></span>

    ```
    Trace folder already exists. Traces will be written tooexisting trace folder: C:\temp\Microsoft.Azure.ServiceFabric.WindowsServer\DeploymentTraces
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

2. <span data-ttu-id="646d5-141">Hello 클러스터 만들기: hello 실행 *CreateServiceFabricCluster.ps1* hello 구성의 각 컴퓨터에서 스크립트 toodeploy hello 서비스 패브릭 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-141">Create hello cluster:  Run hello *CreateServiceFabricCluster.ps1* script toodeploy hello Service Fabric cluster across each machine in hello configuration.</span></span> 
    ```powershell
    .\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -AcceptEULA
    ```

> [!NOTE]
> <span data-ttu-id="646d5-142">배포 추적 toohello VM/컴퓨터 hello CreateServiceFabricCluster.ps1 PowerShell 스크립트를 실행 된 기록 됩니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-142">Deployment traces are written toohello VM/machine on which you ran hello CreateServiceFabricCluster.ps1 PowerShell script.</span></span> <span data-ttu-id="646d5-143">어떤 hello 스크립트를 실행 하는 hello 디렉터리에 hello 하위 먼저 DeploymentTraces 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-143">These can be found in hello subfolder DeploymentTraces, based in hello directory from which hello script was run.</span></span> <span data-ttu-id="646d5-144">서비스 패브릭 되었으면 toosee tooa 컴퓨터 올바르게 배포, 기본 c:\ProgramData\SF) (에 hello 클러스터 구성 파일 FabricSettings 섹션에에서 설명 된 대로 hello FabricDataRoot 디렉터리에서 설치 하는 hello 파일을 찾을 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-144">toosee if Service Fabric was deployed correctly tooa machine, find hello installed files in hello FabricDataRoot directory, as detailed in hello cluster configuration file FabricSettings section (by default c:\ProgramData\SF).</span></span> <span data-ttu-id="646d5-145">또한 작업 관리자에서 실행 중인 FabricHost.exe 및 Fabric.exe 프로세스를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-145">As well, FabricHost.exe and Fabric.exe processes can be seen running in Task Manager.</span></span>
> 
> 

### <a name="step-1c-create-an-offline-internet-disconnected-cluster"></a><span data-ttu-id="646d5-146">1C단계: 오프라인(인터넷 끊김) 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="646d5-146">Step 1C: Create an offline (internet-disconnected) cluster</span></span>
<span data-ttu-id="646d5-147">hello 서비스 패브릭 런타임에서 패키지는 클러스터를 만들 때 자동으로 다운로드 됩니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-147">hello Service Fabric runtime package is automatically downloaded at cluster creation.</span></span> <span data-ttu-id="646d5-148">클러스터 toomachines 하지 배포 toohello을 연결 하는 경우 인터넷 toodownload hello 서비스 패브릭 런타임 이와 별도로, 패키지 및 hello 경로 tooit 클러스터를 만들 때 제공 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-148">When deploying a cluster toomachines not connected toohello internet, you will need toodownload hello Service Fabric runtime package separately, and provide hello path tooit at cluster creation.</span></span>
<span data-ttu-id="646d5-149">hello 런타임 패키지 별도로 다운로드할 수 있습니다, 다른 컴퓨터에서 연결 toohello 인터넷에서 [다운로드 링크-서비스 패브릭 런타임을-Windows Server](https://go.microsoft.com/fwlink/?linkid=839354)합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-149">hello runtime package can be downloaded separately, from another machine connected toohello internet, at [Download Link - Service Fabric Runtime - Windows Server](https://go.microsoft.com/fwlink/?linkid=839354).</span></span> <span data-ttu-id="646d5-150">Hello에서 오프 라인 클러스터를 배포 하 고 실행 하 여 hello 클러스터를 만들 hello 런타임 패키지 toowhere 복사 `CreateServiceFabricCluster.ps1` hello로 `-FabricRuntimePackagePath` 아래와 같이 포함 된 매개 변수:</span><span class="sxs-lookup"><span data-stu-id="646d5-150">Copy hello runtime package toowhere you are deploying hello offline cluster from, and create hello cluster by running `CreateServiceFabricCluster.ps1` with hello `-FabricRuntimePackagePath` parameter included, as shown below:</span></span> 

```powershell
.\CreateServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -FabricRuntimePackagePath .\MicrosoftAzureServiceFabric.cab
```
<span data-ttu-id="646d5-151">여기서 `.\ClusterConfig.json` 및 `.\MicrosoftAzureServiceFabric.cab` 는 각각 hello 경로 toohello 클러스터 구성 및 hello 런타임.cab 파일.</span><span class="sxs-lookup"><span data-stu-id="646d5-151">where `.\ClusterConfig.json` and `.\MicrosoftAzureServiceFabric.cab` are hello paths toohello cluster configuration and hello runtime .cab file respectively.</span></span>


### <a name="step-2-connect-toohello-cluster"></a><span data-ttu-id="646d5-152">2 단계: toohello 클러스터에 연결</span><span class="sxs-lookup"><span data-stu-id="646d5-152">Step 2: Connect toohello cluster</span></span>
<span data-ttu-id="646d5-153">tooconnect tooa 보안 클러스터 참조 [서비스 패브릭 toosecure 클러스터 연결](service-fabric-connect-to-secure-cluster.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-153">tooconnect tooa secure cluster, see [Service fabric connect toosecure cluster](service-fabric-connect-to-secure-cluster.md).</span></span>

<span data-ttu-id="646d5-154">다음 PowerShell 명령을 hello 실행 tooconnect tooan 보안 되지 않은 클러스터:</span><span class="sxs-lookup"><span data-stu-id="646d5-154">tooconnect tooan unsecure cluster, run hello following PowerShell command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <*IPAddressofaMachine*>:<Client connection end point port>
```
<span data-ttu-id="646d5-155">예제:</span><span class="sxs-lookup"><span data-stu-id="646d5-155">Example:</span></span>
```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint 192.13.123.2345:19000
```
### <a name="step-3-bring-up-service-fabric-explorer"></a><span data-ttu-id="646d5-156">3단계: Service Fabric Explorer 표시</span><span class="sxs-lookup"><span data-stu-id="646d5-156">Step 3: Bring up Service Fabric Explorer</span></span>
<span data-ttu-id="646d5-157">서비스 패브릭 탐색기 http://localhost:19080/Explorer/index.html 또는 원격으로 http://&lt hello 컴퓨터 중 하나에서 직접 사용 toohello 클러스터를 연결할 수 있습니다는 이제*IPAddressofaMachine*>: 19080 / Explorer/index.html 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-157">Now you can connect toohello cluster with Service Fabric Explorer either directly from one of hello machines with http://localhost:19080/Explorer/index.html or remotely with http://<*IPAddressofaMachine*>:19080/Explorer/index.html.</span></span>

## <a name="add-and-remove-nodes"></a><span data-ttu-id="646d5-158">노드 추가 및 제거</span><span class="sxs-lookup"><span data-stu-id="646d5-158">Add and remove nodes</span></span>
<span data-ttu-id="646d5-159">추가 하거나 비즈니스 요구 변화에 따라 노드 tooyour 독립 실행형 서비스 패브릭 클러스터를 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-159">You can add or remove nodes tooyour standalone Service Fabric cluster as your business needs change.</span></span> <span data-ttu-id="646d5-160">참조 [더하거나 빼는 노드 tooa 서비스 패브릭 독립 실행형 클러스터](service-fabric-cluster-windows-server-add-remove-nodes.md) 자세한 단계입니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-160">See [Add or Remove nodes tooa Service Fabric standalone cluster](service-fabric-cluster-windows-server-add-remove-nodes.md) for detailed steps.</span></span>

<a id="removecluster" name="removecluster_anchor"></a>
## <a name="remove-a-cluster"></a><span data-ttu-id="646d5-161">클러스터 제거</span><span class="sxs-lookup"><span data-stu-id="646d5-161">Remove a cluster</span></span>
<span data-ttu-id="646d5-162">tooremove 클러스터 hello 실행 *RemoveServiceFabricCluster.ps1* hello 패키지 폴더와 hello 경로 toohello JSON 구성 파일의 단계에서 PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-162">tooremove a cluster, run hello *RemoveServiceFabricCluster.ps1* PowerShell script from hello package folder and pass in hello path toohello JSON configuration file.</span></span> <span data-ttu-id="646d5-163">필요에 따라 hello 삭제의 hello 로그에 대 한 위치를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-163">You can optionally specify a location for hello log of hello deletion.</span></span>

<span data-ttu-id="646d5-164">이 스크립트는 관리자 액세스 tooall hello 컴퓨터 노드로 hello 클러스터 구성 파일에 나열 된 모든 컴퓨터에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-164">This script can be run on any machine that has administrator access tooall hello machines that are listed as nodes in hello cluster configuration file.</span></span> <span data-ttu-id="646d5-165">이 스크립트에서 실행 되는 hello 컴퓨터에는 hello 클러스터의 일부가 toobe 없습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-165">hello machine that this script is run on does not have toobe part of hello cluster.</span></span>

```
# Removes Service Fabric from each machine in hello configuration
.\RemoveServiceFabricCluster.ps1 -ClusterConfigFilePath .\ClusterConfig.json -Force
```

```
# Removes Service Fabric from hello current machine
.\CleanFabric.ps1
```

<a id="telemetry"></a>

## <a name="telemetry-data-collected-and-how-tooopt-out-of-it"></a><span data-ttu-id="646d5-166">원격 분석 데이터 수집 방법과 tooopt 옵트아웃</span><span class="sxs-lookup"><span data-stu-id="646d5-166">Telemetry data collected and how tooopt out of it</span></span>
<span data-ttu-id="646d5-167">기본적으로 hello 제품 hello 서비스 패브릭 사용량 tooimprove hello 제품에서 원격 분석을 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-167">As a default, hello product collects telemetry on hello Service Fabric usage tooimprove hello product.</span></span> <span data-ttu-id="646d5-168">hello hello 설치의 일부분에서는 연결을 확인 너무 처럼 실행 되는 모범 사례 분석기[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1)합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-168">hello Best Practice Analyzer that runs as a part of hello setup checks for connectivity too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1).</span></span> <span data-ttu-id="646d5-169">연결할 수 없는 경우 원격 분석을 취소 하지 않으면 hello 설치가 실패 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-169">If it is not reachable, hello setup fails unless you opt out of telemetry.</span></span>

1. <span data-ttu-id="646d5-170">hello 원격 분석 파이프라인 시도 같은 데이터가 너무 tooupload hello[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) 하루에 한 번입니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-170">hello telemetry pipeline tries tooupload hello following data too[https://vortex.data.microsoft.com/collect/v1](https://vortex.data.microsoft.com/collect/v1) once every day.</span></span> <span data-ttu-id="646d5-171">최상의 노력 업로드 하 고 hello 클러스터 기능에는 영향이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-171">It is a best-effort upload and has no impact on hello cluster functionality.</span></span> <span data-ttu-id="646d5-172">hello 원격 분석만 보내집니다 hello 노드에서 실행 hello 관리자 기본 장애 조치를 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-172">hello telemetry is only sent from hello node that runs hello failover manager primary.</span></span> <span data-ttu-id="646d5-173">다른 노드에서는 원격 분석이 전송되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-173">No other nodes send out telemetry.</span></span>
2. <span data-ttu-id="646d5-174">hello 원격 분석 hello 다음 이루어져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-174">hello telemetry consists of hello following:</span></span>

* <span data-ttu-id="646d5-175">서비스 수</span><span class="sxs-lookup"><span data-stu-id="646d5-175">Number of services</span></span>
* <span data-ttu-id="646d5-176">ServiceTypes 수</span><span class="sxs-lookup"><span data-stu-id="646d5-176">Number of ServiceTypes</span></span>
* <span data-ttu-id="646d5-177">응용 프로그램 수</span><span class="sxs-lookup"><span data-stu-id="646d5-177">Number of Applications</span></span>
* <span data-ttu-id="646d5-178">ApplicationUpgrades 수</span><span class="sxs-lookup"><span data-stu-id="646d5-178">Number of ApplicationUpgrades</span></span>
* <span data-ttu-id="646d5-179">FailoverUnits 수</span><span class="sxs-lookup"><span data-stu-id="646d5-179">Number of FailoverUnits</span></span>
* <span data-ttu-id="646d5-180">InBuildFailoverUnits 수</span><span class="sxs-lookup"><span data-stu-id="646d5-180">Number of InBuildFailoverUnits</span></span>
* <span data-ttu-id="646d5-181">UnhealthyFailoverUnits 수</span><span class="sxs-lookup"><span data-stu-id="646d5-181">Number of UnhealthyFailoverUnits</span></span>
* <span data-ttu-id="646d5-182">복제본 수</span><span class="sxs-lookup"><span data-stu-id="646d5-182">Number of Replicas</span></span>
* <span data-ttu-id="646d5-183">InBuildReplicas 수</span><span class="sxs-lookup"><span data-stu-id="646d5-183">Number of InBuildReplicas</span></span>
* <span data-ttu-id="646d5-184">StandByReplicas 수</span><span class="sxs-lookup"><span data-stu-id="646d5-184">Number of StandByReplicas</span></span>
* <span data-ttu-id="646d5-185">OfflineReplicas 수</span><span class="sxs-lookup"><span data-stu-id="646d5-185">Number of OfflineReplicas</span></span>
* <span data-ttu-id="646d5-186">CommonQueueLength</span><span class="sxs-lookup"><span data-stu-id="646d5-186">CommonQueueLength</span></span>
* <span data-ttu-id="646d5-187">QueryQueueLength</span><span class="sxs-lookup"><span data-stu-id="646d5-187">QueryQueueLength</span></span>
* <span data-ttu-id="646d5-188">FailoverUnitQueueLength</span><span class="sxs-lookup"><span data-stu-id="646d5-188">FailoverUnitQueueLength</span></span>
* <span data-ttu-id="646d5-189">CommitQueueLength</span><span class="sxs-lookup"><span data-stu-id="646d5-189">CommitQueueLength</span></span>
* <span data-ttu-id="646d5-190">노드 수</span><span class="sxs-lookup"><span data-stu-id="646d5-190">Number of Nodes</span></span>
* <span data-ttu-id="646d5-191">IsContextComplete: True/False</span><span class="sxs-lookup"><span data-stu-id="646d5-191">IsContextComplete: True/False</span></span>
* <span data-ttu-id="646d5-192">ClusterId: 각 클러스터에 대해 임의로 생성된 GUID</span><span class="sxs-lookup"><span data-stu-id="646d5-192">ClusterId: This is a GUID randomly generated for each cluster</span></span>
* <span data-ttu-id="646d5-193">ServiceFabricVersion</span><span class="sxs-lookup"><span data-stu-id="646d5-193">ServiceFabricVersion</span></span>
* <span data-ttu-id="646d5-194">Hello 가상 컴퓨터 또는 hello에서 원격 분석을 업로드 하는 컴퓨터의 IP 주소</span><span class="sxs-lookup"><span data-stu-id="646d5-194">IP address of hello virtual machine or machine from which hello telemetry is uploaded</span></span>

<span data-ttu-id="646d5-195">toodisable 원격 분석 hello 너무 다음 추가*속성* 클러스터 config에서: *enableTelemetry: false*합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-195">toodisable telemetry, add hello following too*properties* in your cluster config: *enableTelemetry: false*.</span></span>

<a id="previewfeatures" name="previewfeatures_anchor"></a>

## <a name="preview-features-included-in-this-package"></a><span data-ttu-id="646d5-196">이 패키지에 포함된 미리 보기 기능</span><span class="sxs-lookup"><span data-stu-id="646d5-196">Preview features included in this package</span></span>
<span data-ttu-id="646d5-197">없음.</span><span class="sxs-lookup"><span data-stu-id="646d5-197">None.</span></span>


> [!NOTE]
> <span data-ttu-id="646d5-198">새 hello로 시작 [hello 독립 실행형 Windows Server 클러스터의 GA 버전 (버전 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), 수동 또는 자동으로 클러스터 toofuture 버전에서 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-198">Starting with hello new [GA version of hello standalone cluster for Windows Server (version 5.3.204.x)](https://azure.microsoft.com/blog/azure-service-fabric-for-windows-server-now-ga/), you can upgrade your cluster toofuture releases, manually or automatically.</span></span> <span data-ttu-id="646d5-199">너무 참조[독립 실행형 서비스 패브릭 클러스터 버전 업그레이드](service-fabric-cluster-upgrade-windows-server.md) 대 한 자세한 내용은 문서.</span><span class="sxs-lookup"><span data-stu-id="646d5-199">Refer too[Upgrade a standalone Service Fabric cluster version](service-fabric-cluster-upgrade-windows-server.md) document for details.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="646d5-200">다음 단계</span><span class="sxs-lookup"><span data-stu-id="646d5-200">Next steps</span></span>
* [<span data-ttu-id="646d5-201">PowerShell을 사용하여 응용 프로그램 배포 및 제거</span><span class="sxs-lookup"><span data-stu-id="646d5-201">Deploy and remove applications using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="646d5-202">독립 실행형 Windows 클러스터에 대한 구성 설정</span><span class="sxs-lookup"><span data-stu-id="646d5-202">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="646d5-203">추가 또는 노드 tooa 독립 실행형 서비스 패브릭 클러스터를 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="646d5-203">Add or remove nodes tooa standalone Service Fabric cluster</span></span>](service-fabric-cluster-windows-server-add-remove-nodes.md)
* [<span data-ttu-id="646d5-204">독립 실행형 Service Fabric 클러스터 버전 업그레이드</span><span class="sxs-lookup"><span data-stu-id="646d5-204">Upgrade a standalone Service Fabric cluster version</span></span>](service-fabric-cluster-upgrade-windows-server.md)
* [<span data-ttu-id="646d5-205">Windows를 실행하는 Azure VM에서 독립 실행형 서비스 패브릭 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="646d5-205">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)
* [<span data-ttu-id="646d5-206">Windows 보안을 사용하여 독립 실행형 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="646d5-206">Secure a standalone cluster on Windows using Windows security</span></span>](service-fabric-windows-cluster-windows-security.md)
* [<span data-ttu-id="646d5-207">X509 인증서를 사용하여 Windows에서 독립 실행형 클러스터 보호</span><span class="sxs-lookup"><span data-stu-id="646d5-207">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)

<!--Image references-->
[Trusted Zone]: ./media/service-fabric-cluster-creation-for-windows-server/TrustedZone.png
