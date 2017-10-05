---
title: "Service Fabric 및 Linux에서 컨테이너 배포 | Microsoft Docs"
description: "Service Fabric 및 마이크로 서비스 응용 프로그램 배포를 위한 Linux 컨테이너 사용. 이 문서는 Service Fabric이 컨테이너에 대해 제공하는 기능과 클러스터에 Linux 컨테이너 이미지를 배포하는 방법을 설명합니다."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: 9dcec753e5f999a1bac07276373c0c25f89ec58d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-linux-container-to-service-fabric"></a><span data-ttu-id="8afe4-104">Linux 컨테이너를 Service Fabric에 배포</span><span class="sxs-lookup"><span data-stu-id="8afe4-104">Deploy a Linux container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8afe4-105">Windows 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="8afe4-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="8afe4-106">Linux 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="8afe4-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="8afe4-107">이 문서에서는 Linux의 Docker 컨테이너에서 컨테이너화된 서비스를 빌드하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="8afe4-108">Service Fabric에는 컨테이너화된 마이크로 서비스로 구성된 응용 프로그램을 빌드하는 데 도움을 주는 몇 가지 컨테이너 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="8afe4-109">이를 컨테이너화된 서비스라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-109">These services are called containerized services.</span></span>

<span data-ttu-id="8afe4-110">기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-110">The capabilities include;</span></span>

* <span data-ttu-id="8afe4-111">컨테이너 이미지 배포 및 활성화</span><span class="sxs-lookup"><span data-stu-id="8afe4-111">Container image deployment and activation</span></span>
* <span data-ttu-id="8afe4-112">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="8afe4-112">Resource governance</span></span>
* <span data-ttu-id="8afe4-113">리포지토리 인증</span><span class="sxs-lookup"><span data-stu-id="8afe4-113">Repository authentication</span></span>
* <span data-ttu-id="8afe4-114">포트 매핑을 호스트하는 컨테이너 포트</span><span class="sxs-lookup"><span data-stu-id="8afe4-114">Container port to host port mapping</span></span>
* <span data-ttu-id="8afe4-115">컨테이너 간 검색 및 통신</span><span class="sxs-lookup"><span data-stu-id="8afe4-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="8afe4-116">환경 변수를 구성하고 설정할 수 있는 기능</span><span class="sxs-lookup"><span data-stu-id="8afe4-116">Ability to configure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="8afe4-117">yeoman과 함께 docker 컨테이너 패키징</span><span class="sxs-lookup"><span data-stu-id="8afe4-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="8afe4-118">Linux에서 컨테이너를 패키징할 경우 yeoman 템플릿을 사용하거나 [응용 프로그램 패키지를 수동으로 만들도록](#manually) 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-118">When packaging a container on Linux, you can choose either to use a yeoman template or [create the application package manually](#manually).</span></span>

<span data-ttu-id="8afe4-119">Service Fabric 응용 프로그램은 응용 프로그램의 기능을 제공하는 특정 역할이 있는 하나 이상의 컨테이너를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="8afe4-120">Linux용 Service Fabric SDK는 쉽게 응용 프로그램을 만들고 컨테이너 이미지를 추가할 수 있는 [Yeoman](http://yeoman.io/) 생성기를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-120">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="8afe4-121">Yeoman을 사용하여 *SimpleContainerApp*이라는 단일 Docker 컨테이너가 있는 응용 프로그램을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-121">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="8afe4-122">일반화된 매니페스트 파일을 편집하여 나중에 더 많은 서비스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-122">You can add more services later by editing the generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="8afe4-123">개발 상자에 Docker를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-123">Install Docker on your development box</span></span>

<span data-ttu-id="8afe4-124">다음 명령을 실행하여 Linux 개발 상자에 docker를 설치합니다(OSX에서 vagrant 이미지를 사용하는 경우 docker가 이미 설치되어 있음).</span><span class="sxs-lookup"><span data-stu-id="8afe4-124">Run the following commands to install docker on your Linux development box (if you are using the vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-the-application"></a><span data-ttu-id="8afe4-125">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="8afe4-125">Create the application</span></span>
1. <span data-ttu-id="8afe4-126">터미널에서 `yo azuresfcontainer`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="8afe4-127">응용 프로그램 이름을 지정합니다(예: mycontainerap).</span><span class="sxs-lookup"><span data-stu-id="8afe4-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="8afe4-128">DockerHub 리포지토리에서 컨테이너 이미지에 대한 URL을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-128">Provide the URL for the container image from a DockerHub repo.</span></span> <span data-ttu-id="8afe4-129">이미지 매개변수는 [리포지토리]/[이미지 이름] 양식을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-129">The image parameter takes the form [repo]/[image name]</span></span>
4. <span data-ttu-id="8afe4-130">이미지에 워크로드 진입점이 정의되지 않은 경우 쉼표로 구분된 일련의 명령을 컨테이너 내에서 실행하도록 입력 명령을 명시적으로 지정합니다. 그러면 시작된 후에 컨테이너가 실행되도록 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-130">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

![컨테이너용 Service Fabric Yeoman 생성기][sf-yeoman]

## <a name="deploy-the-application"></a><span data-ttu-id="8afe4-132">응용 프로그램 배포</span><span class="sxs-lookup"><span data-stu-id="8afe4-132">Deploy the application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="8afe4-133">플랫폼 간 CLI 사용</span><span class="sxs-lookup"><span data-stu-id="8afe4-133">Using XPlat CLI</span></span>
<span data-ttu-id="8afe4-134">응용 프로그램이 빌드되면 Azure CLI를 사용하여 로컬 클러스터에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-134">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span></span>

1. <span data-ttu-id="8afe4-135">로컬 Service Fabric 클러스터에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-135">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="8afe4-136">템플릿에 제공된 설치 스크립트를 사용하여 클러스터의 이미지 저장소에 응용 프로그램 패키지를 복사하고 응용 프로그램 유형을 등록하며 응용 프로그램의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-136">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="8afe4-137">브라우저를 열고 http://localhost:19080/Explorer에서 Service Fabric Explorer로 이동합니다(Mac OS X에서 Vagrant를 사용하는 경우 localhost를 VM의 개인 IP로 바꿉니다).</span><span class="sxs-lookup"><span data-stu-id="8afe4-137">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="8afe4-138">응용 프로그램 노드를 확장하면 응용 프로그램 유형에 대한 항목 및 해당 유형의 첫 번째 인스턴스에 대한 다른 항목이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-138">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>
5. <span data-ttu-id="8afe4-139">템플릿에 제공된 제거 스크립트를 사용하여 응용 프로그램 인스턴스를 삭제하고 응용 프로그램 유형을 등록 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-139">Use the uninstall script provided in the template to delete the application instance and unregister the application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="8afe4-140">Azure CLI 2.0 사용</span><span class="sxs-lookup"><span data-stu-id="8afe4-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="8afe4-141">[Azure CLI 2.0을 사용하여 응용 프로그램 수명 주기](service-fabric-application-lifecycle-azure-cli-2-0.md)를 관리하는 방법은 참조 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8afe4-141">See the reference doc on managing an [application life cycle using the Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="8afe4-142">예제 응용 프로그램에 대해서는 [GitHub에서 Service Fabric 컨테이너 코드 샘플을 확인하세요](https://github.com/Azure-Samples/service-fabric-dotnet-containers)(영문).</span><span class="sxs-lookup"><span data-stu-id="8afe4-142">For an example application, [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="8afe4-143">기존 응용 프로그램에 더 많은 서비스 추가</span><span class="sxs-lookup"><span data-stu-id="8afe4-143">Adding more services to an existing application</span></span>

<span data-ttu-id="8afe4-144">`yo`을 사용하여 다른 컨테이너 서비스를 이미 만든 응용 프로그램에 추가하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-144">To add another container service to an application already created using `yo`, perform the following steps:</span></span>

1. <span data-ttu-id="8afe4-145">기존 응용 프로그램의 루트로 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-145">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="8afe4-146">예를 들어 `MyApplication`이 Yeoman에서 만든 응용 프로그램인 경우 `cd ~/YeomanSamples/MyApplication`입니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="8afe4-147">`yo azuresfcontainer:AddService`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="8afe4-148">수동으로 패키징하고 컨테이너 이미지 배포</span><span class="sxs-lookup"><span data-stu-id="8afe4-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="8afe4-149">컨테이너화된 서비스를 수동으로 패키징하는 프로세스는 다음 단계를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="8afe4-150">컨테이너를 리포지토리에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="8afe4-151">패키지 디렉터리 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="8afe4-152">서비스 매니페스트 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="8afe4-153">응용 프로그램 매니페스트 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="8afe4-154">컨테이너 이미지 배포 및 활성화</span><span class="sxs-lookup"><span data-stu-id="8afe4-154">Deploy and activate a container image</span></span>
<span data-ttu-id="8afe4-155">Service Fabric [응용 프로그램 모델](service-fabric-application-model.md)에서 컨테이너는 다수의 서비스 복제본이 배치되는 응용 프로그램 호스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="8afe4-156">컨테이너를 배포하고 활성화하려면 컨테이너 이미지의 이름을 서비스 매니페스트의 `ContainerHost` 요소에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="8afe4-157">서비스 매니페스트에서 진입점용 `ContainerHost`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="8afe4-158">그런 다음 `ImageName`을 컨테이너 리포지토리 및 이미지의 이름이 되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="8afe4-159">다음의 부분 매니페스트는 `myrepo`라는 리포지토리에서 `myimage:v1`라는 컨테이너를 배포하는 방법의 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="8afe4-160">컨테이너 내에서 실행할 쉼표로 구분된 명령 집합과 함께 선택적인 `Commands` 요소를 지정하여 입력 명령을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-160">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span></span>

> [!NOTE]
> <span data-ttu-id="8afe4-161">이미지에 워크로드 진입점이 정의되지 않은 경우 쉼표로 구분된 일련의 명령을 컨테이너 내에서 실행하도록 `Commands` 요소 안의 입력 명령을 명시적으로 지정합니다. 그러면 시작된 후에 컨테이너가 실행되도록 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-161">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands inside `Commands` element with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="8afe4-162">리소스 관리 이해</span><span class="sxs-lookup"><span data-stu-id="8afe4-162">Understand resource governance</span></span>
<span data-ttu-id="8afe4-163">리소스 관리는 호스트에서 컨테이너가 사용할 수 있는 리소스를 제한하는 컨테이너의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="8afe4-164">응용 프로그램 매니페스트에서 지정된 `ResourceGovernancePolicy`는 서비스 코드 패키지에 대한 리소스 제한을 선언하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="8afe4-165">다음 리소스에 대한 리소스 제한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="8afe4-166">메모리</span><span class="sxs-lookup"><span data-stu-id="8afe4-166">Memory</span></span>
* <span data-ttu-id="8afe4-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="8afe4-167">MemorySwap</span></span>
* <span data-ttu-id="8afe4-168">CpuShares(CPU 상대적 가중치)</span><span class="sxs-lookup"><span data-stu-id="8afe4-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="8afe4-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="8afe4-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="8afe4-170">BlkioWeight(BlockIO 상대적 가중치)</span><span class="sxs-lookup"><span data-stu-id="8afe4-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="8afe4-171">향후 릴리스에서는 IOP, 읽기/쓰기 BPS 등과 같은 특정 블록 IO 제한 지정에 대한 지원이 포함될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="8afe4-172">리포지토리 인증</span><span class="sxs-lookup"><span data-stu-id="8afe4-172">Authenticate a repository</span></span>
<span data-ttu-id="8afe4-173">컨테이너를 다운로드하려면 컨테이너 리포지토리에 대한 로그인 자격 증명을 제공해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="8afe4-174">애플리케이션 매니페스트에 지정된 로그인 자격 증명은 로그인 정보 또는 이미지 리포지토리에서 컨테이너 이미지를 다운로드하기 위한 SSH 키를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="8afe4-175">다음 예제는 *TestUser*라는 계정과 암호를 일반 텍스트로 보여줍니다(권장되지 *않음*).</span><span class="sxs-lookup"><span data-stu-id="8afe4-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="8afe4-176">컴퓨터에 배포된 인증서를 사용하여 암호를 암호화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="8afe4-177">다음 예제는 *MyCert*라는 인증서를 사용하여 암호가 암호화된 *TestUser*라는 계정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="8afe4-178">`Invoke-ServiceFabricEncryptText` PowerShell 명령을 사용하여 암호에 대한 암호 텍스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="8afe4-179">자세한 내용은 [Service Fabric 응용 프로그램의 암호 관리](service-fabric-application-secret-management.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8afe4-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="8afe4-180">암호 해독에 사용되는 인증서의 개인 키는 대역외 메서드를 통해 로컬 컴퓨터에 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="8afe4-181">(Azure에서 이 메서드는 Azure Resource Manager입니다.) 그런 다음 Service Fabric이 서비스 패키지를 컴퓨터에 배포하면 암호를 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="8afe4-182">계정 이름과 암호를 사용하면 컨테이너 리포지토리를 통해 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="8afe4-183">컨테이너 포트와 호스트 포트 간 매핑 구성</span><span class="sxs-lookup"><span data-stu-id="8afe4-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="8afe4-184">응용 프로그램 매니페스트에 `PortBinding`을 지정하여 컨테이너와의 통신에 사용되는 호스트 포트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="8afe4-185">포트 바인딩은 컨테이너 내에서 서비스가 수신 대기 중인 포트를 호스트의 포트로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="8afe4-186">컨테이너 간 검색 및 통신 구성</span><span class="sxs-lookup"><span data-stu-id="8afe4-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="8afe4-187">`PortBinding` 정책을 사용하면 컨테이너 포트를 서비스 매니페스트의 `Endpoint`에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-187">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest.</span></span> <span data-ttu-id="8afe4-188">끝점 `Endpoint1`(예: 포트 80)은 고정 포트를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-188">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="8afe4-189">어떤 포트도 지정하지 않을 수 있는데, 그런 경우 클러스터의 응용 프로그램 포트 범위에서 포트가 무작위로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="8afe4-190">게스트 컨테이너의 서비스 매니페스트에서 `Endpoint` 태그를 사용하여 끝점을 지정하는 경우 Service Fabric은 이 끝점을 명명 서비스에 자동으로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="8afe4-191">클러스터에서 실행되는 기타 서비스는 해결용 REST 쿼리를 사용하여 이 컨테이너를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

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

<span data-ttu-id="8afe4-192">명명 서비스에 등록하면 [역방향 프록시](service-fabric-reverseproxy.md)를 사용하여 컨테이너 내 코드를 통해 쉽게 컨테이너 간 통신을 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-192">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="8afe4-193">역방향 프록시 http 수신 대기 포트와 통신하려는 서비스 이름을 환경 변수로서 제공하면 통신이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="8afe4-194">자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8afe4-194">For more information, see the next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="8afe4-195">환경 변수 구성 및 설정</span><span class="sxs-lookup"><span data-stu-id="8afe4-195">Configure and set environment variables</span></span>
<span data-ttu-id="8afe4-196">환경 변수는 컨테이너에 배포된 서비스나 프로세스/게스트 실행 파일로서 배포된 서비스를 위해 서비스 매니페스트의 각 코드 패키지에 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-196">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="8afe4-197">이러한 환경 변수 값은 응용 프로그램 매니페스트에서 명확하게 재정의되거나 응용 프로그램 매개 변수로 배포하는 동안 지정될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-197">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="8afe4-198">다음 서비스 매니페스트 XML 코드 조각은 코드 패키지에 대한 환경 변수를 지정하는 방법의 예제를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-198">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="8afe4-199">이러한 환경 변수는 응용 프로그램 매니페스트 수준에서 재정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-199">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="8afe4-200">이전 예제에서 `HttpGateway` 환경 변수(19000)에는 명확한 값을 지정했던 반면에 `BackendServiceName` 매개 변수의 값은 `[BackendSvc]` 응용 프로그램 매개 변수를 통해 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-200">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="8afe4-201">이렇게 설정하면 응용 프로그램을 배포하고 매니페스트에 고정된 값을 지정하지 않은 경우 `BackendServiceName`에 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-201">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="8afe4-202">응용 프로그램 및 서비스 매니페스트에 대한 전체 예제</span><span class="sxs-lookup"><span data-stu-id="8afe4-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="8afe4-203">예제 응용 프로그램 매니페스트는 다음을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="8afe4-204">예제 서비스 매니페스트(이전 응용 프로그램 매니페스트에 지정됨)는 다음을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="8afe4-204">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="8afe4-205">다음 단계</span><span class="sxs-lookup"><span data-stu-id="8afe4-205">Next steps</span></span>
<span data-ttu-id="8afe4-206">컨테이너화된 서비스를 배포했으므로 [Service Fabric 응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)를 읽고 수명 주기를 관리하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="8afe4-206">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="8afe4-207">Service Fabric 및 컨테이너 개요</span><span class="sxs-lookup"><span data-stu-id="8afe4-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="8afe4-208">Azure CLI를 사용하여 Service Fabric 클러스터와 상호 작용</span><span class="sxs-lookup"><span data-stu-id="8afe4-208">Interacting with Service Fabric clusters using the Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="8afe4-209">관련된 문서</span><span class="sxs-lookup"><span data-stu-id="8afe4-209">Related articles</span></span>

* [<span data-ttu-id="8afe4-210">Service Fabric 및 Azure CLI 2.0 시작</span><span class="sxs-lookup"><span data-stu-id="8afe4-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="8afe4-211">Service Fabric 및 XPlat CLI 시작</span><span class="sxs-lookup"><span data-stu-id="8afe4-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
