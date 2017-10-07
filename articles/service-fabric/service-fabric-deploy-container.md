---
title: "aaaService 패브릭 및 컨테이너를 배포 합니다. | Microsoft Docs"
description: "서비스 패브릭 및 hello 컨테이너 toodeploy 마이크로 서비스 응용 프로그램의 사용합니다. 이 문서는 컨테이너 및 어떻게 toodeploy Windows 컨테이너는 클러스터로을 이미지에 대 한 서비스 패브릭 제공 하는 hello 기능에 설명 합니다."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="58655-104">Windows 컨테이너 tooService 패브릭 배포</span><span class="sxs-lookup"><span data-stu-id="58655-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="58655-105">Windows 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="58655-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="58655-106">Docker 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="58655-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="58655-107">이 문서는 hello Windows 컨테이너에서 컨테이너 화 된 서비스를 만드는 과정을 안내 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="58655-108">Service Fabric에는 컨테이너 내에서 실행되는 마이크로 서비스로 구성된 응용 프로그램을 빌드하는 데 도움을 주는 몇 가지 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="58655-109">hello 기능 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58655-109">hello capabilities include:</span></span>

* <span data-ttu-id="58655-110">컨테이너 이미지 배포 및 활성화</span><span class="sxs-lookup"><span data-stu-id="58655-110">Container image deployment and activation</span></span>
* <span data-ttu-id="58655-111">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="58655-111">Resource governance</span></span>
* <span data-ttu-id="58655-112">리포지토리 인증</span><span class="sxs-lookup"><span data-stu-id="58655-112">Repository authentication</span></span>
* <span data-ttu-id="58655-113">컨테이너 포트와 호스트 포트 간 매핑</span><span class="sxs-lookup"><span data-stu-id="58655-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="58655-114">컨테이너 간 검색 및 통신</span><span class="sxs-lookup"><span data-stu-id="58655-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="58655-115">기능 tooconfigure 환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="58655-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="58655-116">응용 프로그램에 포함 하는 컨테이너 화 된 서비스 toobe 패키징하는 경우 각 기능은 작동 방식을 살펴 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="58655-117">Windows 컨테이너 패키징</span><span class="sxs-lookup"><span data-stu-id="58655-117">Package a Windows container</span></span>
<span data-ttu-id="58655-118">컨테이너를 압축할 때 선택할 수 있습니다 toouse Visual Studio 프로젝트 템플릿 또는 [hello 응용 프로그램 패키지를 수동으로 만들](#manually)합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="58655-119">Visual Studio, hello 응용 프로그램 패키지 구조를 사용 하 고 매니페스트 파일을 만듭니다에서 hello 새 프로젝트 템플릿이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="58655-120">hello 가장 쉬운 방법은 toopackage를 서비스에 기존 컨테이너 이미지는 Visual Studio toouse입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="58655-121">Visual Studio toopackage 기존 컨테이너 이미지를 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="58655-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="58655-122">Visual Studio는 서비스 패브릭 서비스 템플릿 toohelp을 컨테이너 tooa 서비스 패브릭 클러스터를 배포 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="58655-123">**파일** > **새 프로젝트**를 선택하여 Service Fabric 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58655-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="58655-124">선택 **게스트 컨테이너** hello 서비스 템플릿으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="58655-125">선택 **이미지 이름** 저장소 컨테이너에서에서 hello 경로 toohello 이미지를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="58655-126">예를 들어 https://hub.docker.com에서 `myrepo/myimage:v1`입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="58655-127">서비스에 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="58655-128">컨테이너 화 된 서비스 끝점 통신을 위해 필요로 한다면 hello 프로토콜, 포트 및 형식 toohello ServiceManifest.xml 파일 이제 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="58655-129">예:</span><span class="sxs-lookup"><span data-stu-id="58655-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="58655-130">Hello를 제공 하 여 `UriScheme`, 서비스 패브릭 명명 서비스 검색 기능에 대 한 hello로 hello 컨테이너 끝점을 자동으로 등록 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="58655-131">hello 포트 (에서처럼 앞 예제는 hello)를 고정 또는 동적으로 할당 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="58655-132">포트를 지정 하지 (처럼 모든 서비스와 함께) hello 응용 프로그램 포트 범위에서 할당 동적으로 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58655-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="58655-133">또한 tooconfigure hello 컨테이너 toohost 포트 매핑을 지정 하 여 필요한는 `PortBinding` hello 응용 프로그램 매니페스트에서 정책입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="58655-134">자세한 내용은 참조 [컨테이너 toohost 포트 매핑 구성](#Portsection)합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="58655-135">컨테이너에 리소스 관리가 필요할 경우 `ResourceGovernancePolicy`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="58655-136">컨테이너와 개인 리포지토리에 tooauthenticate를 필요한 경우 다음 추가 `RepositoryCredentials`합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="58655-137">컨테이너 지원이 설정 된 Windows Server 2016 컴퓨터에서 실행 하는 경우에 hello 패키지를 사용 하 고 작업 toodeploy tooyour 로컬 클러스터를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="58655-138">준비가 되 면 원격 클러스터를 tooa hello 응용 프로그램을 게시 하거나 hello 솔루션 toosource 컨트롤에서 확인 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="58655-139">예를 들어, 체크 아웃 hello에 대 한 [GitHub에서 서비스 패브릭 컨테이너 코드 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="58655-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="58655-140">Windows Server 2016 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="58655-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="58655-141">toodeploy 컨테이너 화 된 응용 프로그램 해야 toocreate 컨테이너를 지 원하는 Windows Server 2016을 실행 하는 클러스터를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="58655-142">클러스터는 로컬로 실행되거나 Azure에서 Azure Resource Manager를 통해 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="58655-143">Azure 리소스 관리자를 사용 하는 클러스터 toodeploy 선택 hello **컨테이너와 Windows Server 2016** 이미지 Azure의 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="58655-144">Hello 문서 참조 [Azure 리소스 관리자를 사용 하 여 서비스 패브릭 클러스터를 만들](service-fabric-cluster-creation-via-arm.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="58655-145">Azure 리소스 관리자 설정에 따라 hello를 사용 하는 것을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="58655-146">Hello를 사용할 수도 있습니다 [5 노드 Azure 리소스 관리자 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate 클러스터입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="58655-147">또는 Service Fabric 및 Windows 컨테이너 사용에 대한 커뮤니티 [블로그 게시물](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="58655-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="58655-148">수동으로 패키징하고 컨테이너 이미지 배포</span><span class="sxs-lookup"><span data-stu-id="58655-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="58655-149">수동으로 컨테이너 화 된 서비스를 패키지의 hello 프로세스 단계를 수행 하는 hello를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="58655-150">Hello 컨테이너 tooyour 리포지토리를 게시 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="58655-151">Hello 패키지 디렉터리 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58655-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="58655-152">Hello 서비스 매니페스트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="58655-153">Hello 응용 프로그램 매니페스트 파일을 편집 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="58655-154">컨테이너 이미지 배포 및 활성화</span><span class="sxs-lookup"><span data-stu-id="58655-154">Deploy and activate a container image</span></span>
<span data-ttu-id="58655-155">서비스 패브릭 hello에 [응용 프로그램 모델](service-fabric-application-model.md), 컨테이너 되는 여러 서비스 복제본을 배치 하는 응용 프로그램 호스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="58655-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="58655-156">toodeploy hello 컨테이너 이미지의 put hello 이름, 컨테이너를 활성화 하 고는 `ContainerHost` hello 서비스 매니페스트의 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="58655-157">Hello 서비스 매니페스트에 추가 된 `ContainerHost` hello 진입점에 대 한 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="58655-158">그런 다음 세트 hello `ImageName` toobe hello 이름 hello 컨테이너 리포지토리 및 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="58655-159">hello 다음 부분 매니페스트가의 예가 나와 toodeploy hello 컨테이너 호출 하는 방법을 `myimage:v1` 라는 리포지토리에서 `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="58655-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

<span data-ttu-id="58655-160">선택적 명령 toorun hello 컨테이너에서 hello 시작 시 지정할 수 있습니다 `Commands` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="58655-161">여러 명령의 경우 쉼표로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="58655-162">리소스 관리 이해</span><span class="sxs-lookup"><span data-stu-id="58655-162">Understand resource governance</span></span>
<span data-ttu-id="58655-163">리소스 관리는 hello 호스트에서 컨테이너 hello hello 리소스를 제한 하는 hello 컨테이너의 기능을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="58655-164">hello `ResourceGovernancePolicy`, 서비스 코드 패키지에 대 한 사용 되는 toodeclare 리소스 제한을 hello 응용 프로그램 매니페스트에서 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="58655-165">다음 리소스는 hello에 대 한 리소스 제한은 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="58655-166">메모리</span><span class="sxs-lookup"><span data-stu-id="58655-166">Memory</span></span>
* <span data-ttu-id="58655-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="58655-167">MemorySwap</span></span>
* <span data-ttu-id="58655-168">CpuShares(CPU 상대적 가중치)</span><span class="sxs-lookup"><span data-stu-id="58655-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="58655-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="58655-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="58655-170">BlkioWeight(BlockIO 상대적 가중치)</span><span class="sxs-lookup"><span data-stu-id="58655-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="58655-171">IOP, 읽기/쓰기 BPS 등과 같은 특정 블록 IO 제한 지정에 대한 지원이 향후 릴리스에 예정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
> 
> 

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a><span data-ttu-id="58655-172">리포지토리 인증</span><span class="sxs-lookup"><span data-stu-id="58655-172">Authenticate a repository</span></span>
<span data-ttu-id="58655-173">컨테이너 toodownload tooprovide 로그인 자격 증명 toohello 컨테이너 리포지토리를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="58655-174">hello 로그인 자격 증명을 hello 응용 프로그램 매니페스트에 지정은 사용 되는 toospecify hello 로그인 정보, 또는 hello 이미지 리포지토리에서 hello 컨테이너 이미지를 다운로드 하기 위한 SSH 키입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="58655-175">hello 다음 예제에서는 호출 계정을 *TestUser* hello 암호를 일반 텍스트로 함께 (*하지* 권장):</span><span class="sxs-lookup"><span data-stu-id="58655-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

<span data-ttu-id="58655-176">Toohello 컴퓨터 배포 된 인증서를 사용 하 여 hello 암호를 암호화 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="58655-177">hello 다음 예제에서는 호출 계정을 *TestUser*이라는 인증서를 사용 하 여 hello 암호를 암호화 하는 경우, *MyCert*합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="58655-178">Hello를 사용할 수 있습니다 `Invoke-ServiceFabricEncryptText` hello 암호에 대 한 PowerShell 명령 toocreate hello 비밀 암호화 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="58655-179">자세한 내용은 hello 문서 참조 [서비스 패브릭 응용 프로그램의 암호 관리](service-fabric-application-secret-management.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="58655-180">hello toodecrypt hello 암호를 사용 하는 hello 인증서의 개인 키 대역의 메서드에서 배포 toohello 로컬 컴퓨터 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="58655-181">(Azure에서 이 메서드는 Azure Resource Manager입니다.) 그런 다음 서비스 패브릭 hello 서비스 패키지 toohello 컴퓨터를 배포 하면 hello 암호를 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="58655-182">Hello 계정 이름과 함께 hello 암호를 사용 하 여 다음 hello 컨테이너 리포지토리와 상호 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <span data-ttu-id="58655-183"><a name ="Portsection"></a>컨테이너 toohost 포트 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="58655-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="58655-184">지정 하 여 hello 컨테이너와 호스트 사용 되는 포트 toocommunicate를 구성할 수 있습니다는 `PortBinding` hello 응용 프로그램 매니페스트에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="58655-185">hello 포트 바인딩 지도 hello 포트 toowhich hello 서비스는 hello 컨테이너 tooa 호스트의 포트에 hello 내 수신 대기 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="58655-186">컨테이너 간 검색 및 통신 구성</span><span class="sxs-lookup"><span data-stu-id="58655-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="58655-187">Hello를 사용할 수 있습니다 `PortBinding` 요소 toomap hello 서비스 매니페스트의 컨테이너 포트 tooan 끝점입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="58655-188">다음 예제는 hello에서 끝점 hello `Endpoint1` 8905 고정된 포트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="58655-189">지정할 수도 있습니다 포트 하지 전혀 있습니다을 위해 hello 클러스터의 응용 프로그램 포트 범위에서 임의 포트를 선택한 경우.</span><span class="sxs-lookup"><span data-stu-id="58655-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```
<span data-ttu-id="58655-190">Hello를 사용 하 여 끝점을 지정 하는 경우 `Endpoint` 게스트 컨테이너 서비스 패브릭의 hello 서비스 매니페스트에서 태그를에서 자동으로이 끝점 toohello 명명 서비스를 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="58655-191">Hello 클러스터에서 실행 되는 다른 서비스를 확인 하기 위한 hello REST 쿼리를 사용 하 여이 컨테이너를 검색할 따라서 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="58655-192">Hello 명명 서비스를 등록 하면 수행할 수 있습니다 컨테이너-컨테이너 통신 내 컨테이너에서 hello를 사용 하 여 [역방향 프록시](service-fabric-reverseproxy.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="58655-193">통신은 hello 역방향 프록시 http 수신 포트 및 환경 변수로 toocommunicate 원하는 hello 서비스의 hello 이름을 제공 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58655-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="58655-194">자세한 내용은 hello 다음 섹션을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="58655-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="58655-195">환경 변수 구성 및 설정</span><span class="sxs-lookup"><span data-stu-id="58655-195">Configure and set environment variables</span></span>
<span data-ttu-id="58655-196">각 코드 패키지 서비스 매니페스트 hello에에서 대 한 환경 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="58655-197">이 기능은 컨테이너 또는 프로세스 또는 게스트 실행 파일로 배포되는지 여부에 관계 없이 모든 서비스에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="58655-198">Hello 응용 프로그램에서 값 매니페스트 또는 응용 프로그램 매개 변수를 배포 하는 동안 지정 환경 변수를 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="58655-199">hello 다음 서비스 매니페스트 XML 조각 표시 방법의 예제 코드 패키지에 대 한 toospecify 환경 변수:</span><span class="sxs-lookup"><span data-stu-id="58655-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

<span data-ttu-id="58655-200">이러한 환경 변수는 hello 응용 프로그램 매니페스트 수준에서 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="58655-201">Hello에 대 한 명시적 값을 지정 했기 hello 이전 예에서 `HttpGateway` 환경 변수 (19000), hello 값을 설정 하는 동안 `BackendServiceName` hello 통해 매개 변수 `[BackendSvc]` 응용 프로그램 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="58655-202">이 설정을 통해 toospecify hello 값에 대 한 `BackendServiceName`hello 응용 프로그램을 배포 하 고 hello 매니페스트에 고정된 값이 없는 값입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="58655-203">격리 모드 구성</span><span class="sxs-lookup"><span data-stu-id="58655-203">Configure isolation mode</span></span>

<span data-ttu-id="58655-204">Windows는 컨테이너 - 프로세스 및 Hyper-V에 대한 두 가지 격리 모드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="58655-205">Hello 프로세스 격리 모드에서 실행 되는 모든 hello 컨테이너 hello 호스트와 동일한 호스트 컴퓨터 공유 hello 커널을 hello 합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="58655-206">Hello Hyper-v 격리 모드에서 hello 커널 각 Hyper-v 컨테이너와 hello 컨테이너 호스트 간에 격리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58655-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="58655-207">hello 격리 모드 hello에 지정 된 `ContainerHostPolicies` hello 응용 프로그램 매니페스트 파일의 태그입니다.</span><span class="sxs-lookup"><span data-stu-id="58655-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="58655-208">지정할 수 있는 hello 격리 모드는 `process`, `hyperv`, 및 `default`합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="58655-209">hello `default` 격리 모드 기본값 너무`process` Windows 서버에서 호스팅하고 너무 기본값`hyperv` Windows 10 호스트에서.</span><span class="sxs-lookup"><span data-stu-id="58655-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="58655-210">hello 다음 코드 조각에서는 hello 격리 모드 hello 응용 프로그램 매니페스트 파일에 지정 되는 방법을</span><span class="sxs-lookup"><span data-stu-id="58655-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="58655-211">응용 프로그램 및 서비스 매니페스트에 대한 전체 예제</span><span class="sxs-lookup"><span data-stu-id="58655-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="58655-212">예제 응용 프로그램 매니페스트는 다음을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="58655-212">An example application manifest follows:</span></span>

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

<span data-ttu-id="58655-213">(Hello 응용 프로그램 매니페스트를 앞에 지정 된) 예제 서비스 매니페스트는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58655-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a><span data-ttu-id="58655-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="58655-214">Next steps</span></span>
<span data-ttu-id="58655-215">이제는 컨테이너 화 된 서비스를 배포한 자세히 배울 방법 toomanage 읽어 주기 [서비스 패브릭 응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="58655-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="58655-216">Service Fabric 및 컨테이너 개요</span><span class="sxs-lookup"><span data-stu-id="58655-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="58655-217">예제는 [GitHub에서 Service Fabric 컨테이너 코드 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="58655-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
