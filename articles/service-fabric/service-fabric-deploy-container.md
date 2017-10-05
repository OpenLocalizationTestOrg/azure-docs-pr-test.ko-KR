---
title: "Service Fabric 및 컨테이너 배포 | Microsoft Docs"
description: "Service Fabric 및 마이크로 서비스 응용 프로그램 배포를 위한 컨테이너 사용. 이 문서는 Service Fabric이 컨테이너에 대해 제공하는 기능과 클러스터에 Windows 컨테이너 이미지를 배포하는 방법을 설명합니다."
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
ms.openlocfilehash: 25d6b056421e71fa70ed20a39589f77dbbc25c69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-windows-container-to-service-fabric"></a><span data-ttu-id="ff370-104">Windows 컨테이너를 Service Fabric에 배포</span><span class="sxs-lookup"><span data-stu-id="ff370-104">Deploy a Windows container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ff370-105">Windows 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="ff370-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="ff370-106">Docker 컨테이너 배포</span><span class="sxs-lookup"><span data-stu-id="ff370-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="ff370-107">이 문서에서는 Windows 컨테이너에서 컨테이너화된 서비스를 빌드하는 과정을 안내합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-107">This article walks you through the process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="ff370-108">Service Fabric에는 컨테이너 내에서 실행되는 마이크로 서비스로 구성된 응용 프로그램을 빌드하는 데 도움을 주는 몇 가지 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="ff370-109">기능은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-109">The capabilities include:</span></span>

* <span data-ttu-id="ff370-110">컨테이너 이미지 배포 및 활성화</span><span class="sxs-lookup"><span data-stu-id="ff370-110">Container image deployment and activation</span></span>
* <span data-ttu-id="ff370-111">리소스 관리</span><span class="sxs-lookup"><span data-stu-id="ff370-111">Resource governance</span></span>
* <span data-ttu-id="ff370-112">리포지토리 인증</span><span class="sxs-lookup"><span data-stu-id="ff370-112">Repository authentication</span></span>
* <span data-ttu-id="ff370-113">컨테이너 포트와 호스트 포트 간 매핑</span><span class="sxs-lookup"><span data-stu-id="ff370-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="ff370-114">컨테이너 간 검색 및 통신</span><span class="sxs-lookup"><span data-stu-id="ff370-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="ff370-115">환경 변수를 구성하고 설정할 수 있는 기능</span><span class="sxs-lookup"><span data-stu-id="ff370-115">Ability to configure and set environment variables</span></span>

<span data-ttu-id="ff370-116">응용 프로그램에 포함할 컨테이너화된 서비스를 패키징하는 경우 각 기능이 어떻게 작동하는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-116">Let's look at how each of capabilities works when you're packaging a containerized service to be included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="ff370-117">Windows 컨테이너 패키징</span><span class="sxs-lookup"><span data-stu-id="ff370-117">Package a Windows container</span></span>
<span data-ttu-id="ff370-118">컨테이너를 패키징할 경우 Visual Studio 프로젝트 템플릿을 사용하거나 [응용 프로그램 패키지를 수동으로 만들도록](#manually)선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-118">When you package a container, you can choose to use either a Visual Studio project template or [create the application package manually](#manually).</span></span>  <span data-ttu-id="ff370-119">Visual Studio를 사용하면 새 프로젝트 템플릿에 의해 응용 프로그램 패키지 구조 및 매니페스트 파일이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-119">When you use Visual Studio, the application package structure and manifest files are created by the New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="ff370-120">기존 컨테이너 이미지를 서비스로 패키징하는 가장 쉬운 방법은 Visual Studio를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-120">The easiest way to package an existing container image into a service is to use Visual Studio.</span></span>

## <a name="use-visual-studio-to-package-an-existing-container-image"></a><span data-ttu-id="ff370-121">Visual Studio를 사용하여 기존 컨테이너 이미지 패키징</span><span class="sxs-lookup"><span data-stu-id="ff370-121">Use Visual Studio to package an existing container image</span></span>
<span data-ttu-id="ff370-122">Visual Studio는 컨테이너를 Service Fabric 클러스터에 배포할 수 있도록 Service Fabric 서비스 템플릿을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-122">Visual Studio provides a Service Fabric service template to help you deploy a container to a Service Fabric cluster.</span></span>

1. <span data-ttu-id="ff370-123">**파일** > **새 프로젝트**를 선택하여 Service Fabric 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="ff370-124">**게스트 컨테이너**를 서비스 템플릿으로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-124">Choose **Guest Container** as the service template.</span></span>
3. <span data-ttu-id="ff370-125">**이미지 이름**을 선택하고 컨테이너 리포지토리의 이미지 경로를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-125">Choose **Image Name** and provide the path to the image in your container repository.</span></span> <span data-ttu-id="ff370-126">예를 들어 https://hub.docker.com에서 `myrepo/myimage:v1`입니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="ff370-127">서비스에 이름을 지정하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="ff370-128">컨테이너화된 서비스에서 통신에 끝점이 필요한 경우 이제 프로토콜, 포트, 형식을 ServiceManifest.xml 파일에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-128">If your containerized service needs an endpoint for communication, you can now add the protocol, port, and type to the ServiceManifest.xml file.</span></span> <span data-ttu-id="ff370-129">예:</span><span class="sxs-lookup"><span data-stu-id="ff370-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="ff370-130">`UriScheme`을 입력하여 Service Fabric은 이 컨테이너 끝점이 검색될 수 있도록 이름 지정 서비스에 자동으로 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-130">By providing the `UriScheme`, Service Fabric automatically registers the container endpoint with the Naming service for discoverability.</span></span> <span data-ttu-id="ff370-131">포트는 고정되거나(앞의 예제에 표시된 것과 같이) 동적으로 할당될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-131">The port can either be fixed (as shown in the preceding example) or dynamically allocated.</span></span> <span data-ttu-id="ff370-132">포트를 지정하지 않는 경우 응용 프로그램 포트 범위에서 동적으로 할당됩니다(모든 서비스와 함께 발생하므로).</span><span class="sxs-lookup"><span data-stu-id="ff370-132">If you don't specify a port, it is dynamically allocated from the application port range (as would happen with any service).</span></span>
    <span data-ttu-id="ff370-133">또한 응용 프로그램 매니페스트에 `PortBinding` 정책을 지정하여 컨테이너를 호스트 포트 매핑으로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-133">You also need to configure the container to host port mapping by specifying a `PortBinding` policy in the application manifest.</span></span> <span data-ttu-id="ff370-134">자세한 내용은 [컨테이너를 호스트 포트 매핑으로 구성](#Portsection)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff370-134">For more information, see [Configure container to host port mapping](#Portsection).</span></span>
6. <span data-ttu-id="ff370-135">컨테이너에 리소스 관리가 필요할 경우 `ResourceGovernancePolicy`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="ff370-136">컨테이너가 개인 리포지토리에 인증해야 하는 경우 `RepositoryCredentials`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-136">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="ff370-137">컨테이너 지원이 설정된 Windows Server 2016 컴퓨터에서 실행하는 경우 패키지를 사용하고 로컬 클러스터에 배포하는 작업을 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use the package and publish action to deploy to your local cluster.</span></span> 
8. <span data-ttu-id="ff370-138">준비가 되면 원격 클러스터로 응용 프로그램을 게시하거나 원본 제어에 대한 솔루션을 체크 인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-138">When ready, you can publish the application to a remote cluster or check in the solution to source control.</span></span> 

<span data-ttu-id="ff370-139">예제는 [GitHub에서 Service Fabric 컨테이너 코드 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ff370-139">For an example, checkout the [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="ff370-140">Windows Server 2016 클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="ff370-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="ff370-141">컨테이너화된 응용 프로그램을 배포하려면 컨테이너 지원이 설정된 Windows Server 2016이 실행되는 클러스터를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-141">To deploy your containerized application, you need to create a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="ff370-142">클러스터는 로컬로 실행되거나 Azure에서 Azure Resource Manager를 통해 배포될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="ff370-143">Azure Resource Manager를 사용하여 클러스터를 배포하려면 Azure에서 **Windows Server 2016(컨테이너 포함)** 이미지 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-143">To deploy a cluster using Azure Resource Manager, choose the **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="ff370-144">문서 [Azure Resource Manager를 사용하여 Service Fabric 클러스터 만들기](service-fabric-cluster-creation-via-arm.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff370-144">See the article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="ff370-145">다음 Azure Resource Manager 설정을 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-145">Ensure that you use the following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="ff370-146">[Five Node Azure Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype)을 사용하여 클러스터를 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-146">You can also use the [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) to create a cluster.</span></span> <span data-ttu-id="ff370-147">또는 Service Fabric 및 Windows 컨테이너 사용에 대한 커뮤니티 [블로그 게시물](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff370-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="ff370-148">수동으로 패키징하고 컨테이너 이미지 배포</span><span class="sxs-lookup"><span data-stu-id="ff370-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="ff370-149">컨테이너화된 서비스를 수동으로 패키징하는 프로세스는 다음 단계를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="ff370-150">컨테이너를 리포지토리에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="ff370-151">패키지 디렉터리 구조를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="ff370-152">서비스 매니페스트 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="ff370-153">응용 프로그램 매니페스트 파일을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="ff370-154">컨테이너 이미지 배포 및 활성화</span><span class="sxs-lookup"><span data-stu-id="ff370-154">Deploy and activate a container image</span></span>
<span data-ttu-id="ff370-155">Service Fabric [응용 프로그램 모델](service-fabric-application-model.md)에서 컨테이너는 다수의 서비스 복제본이 배치되는 응용 프로그램 호스트를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="ff370-156">컨테이너를 배포하고 활성화하려면 컨테이너 이미지의 이름을 서비스 매니페스트의 `ContainerHost` 요소에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="ff370-157">서비스 매니페스트에서 진입점용 `ContainerHost`를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="ff370-158">그런 다음 `ImageName`을 컨테이너 리포지토리 및 이미지의 이름이 되도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="ff370-159">다음의 부분 매니페스트는 `myrepo`라는 리포지토리에서 `myimage:v1`라는 컨테이너를 배포하는 방법의 예를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="ff370-160">옵션 명령을 지정하여 `Commands` 요소에서 컨테이너 시작을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-160">You can specify optional commands to run upon starting the container under the `Commands` element.</span></span> <span data-ttu-id="ff370-161">여러 명령의 경우 쉼표로 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="ff370-162">리소스 관리 이해</span><span class="sxs-lookup"><span data-stu-id="ff370-162">Understand resource governance</span></span>
<span data-ttu-id="ff370-163">리소스 관리는 호스트에서 컨테이너가 사용할 수 있는 리소스를 제한하는 컨테이너의 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="ff370-164">응용 프로그램 매니페스트에서 지정된 `ResourceGovernancePolicy`는 서비스 코드 패키지에 대한 리소스 제한을 선언하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="ff370-165">다음 리소스에 대한 리소스 제한을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="ff370-166">메모리</span><span class="sxs-lookup"><span data-stu-id="ff370-166">Memory</span></span>
* <span data-ttu-id="ff370-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="ff370-167">MemorySwap</span></span>
* <span data-ttu-id="ff370-168">CpuShares(CPU 상대적 가중치)</span><span class="sxs-lookup"><span data-stu-id="ff370-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="ff370-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="ff370-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="ff370-170">BlkioWeight(BlockIO 상대적 가중치)</span><span class="sxs-lookup"><span data-stu-id="ff370-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="ff370-171">IOP, 읽기/쓰기 BPS 등과 같은 특정 블록 IO 제한 지정에 대한 지원이 향후 릴리스에 예정되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="ff370-172">리포지토리 인증</span><span class="sxs-lookup"><span data-stu-id="ff370-172">Authenticate a repository</span></span>
<span data-ttu-id="ff370-173">컨테이너를 다운로드하려면 컨테이너 리포지토리에 대한 로그인 자격 증명을 제공해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="ff370-174">애플리케이션 매니페스트에 지정된 로그인 자격 증명은 로그인 정보 또는 이미지 리포지토리에서 컨테이너 이미지를 다운로드하기 위한 SSH 키를 지정하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="ff370-175">다음 예제는 *TestUser*라는 계정과 암호를 일반 텍스트로 보여줍니다(권장되지 *않음*).</span><span class="sxs-lookup"><span data-stu-id="ff370-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="ff370-176">컴퓨터에 배포된 인증서를 사용하여 암호를 암호화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="ff370-177">다음 예제는 *MyCert*라는 인증서를 사용하여 암호가 암호화된 *TestUser*라는 계정을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="ff370-178">`Invoke-ServiceFabricEncryptText` PowerShell 명령을 사용하여 암호에 대한 암호 텍스트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="ff370-179">자세한 내용은 [Service Fabric 응용 프로그램의 암호 관리](service-fabric-application-secret-management.md) 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff370-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="ff370-180">암호 해독에 사용되는 인증서의 개인 키는 대역외 메서드를 통해 로컬 컴퓨터에 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="ff370-181">(Azure에서 이 메서드는 Azure Resource Manager입니다.) 그런 다음 Service Fabric이 서비스 패키지를 컴퓨터에 배포하면 암호를 해독할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="ff370-182">계정 이름과 암호를 사용하면 컨테이너 리포지토리를 통해 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <span data-ttu-id="ff370-183"><a name ="Portsection"></a> 컨테이너를 호스트 포트 매핑에 구성</span><span class="sxs-lookup"><span data-stu-id="ff370-183"><a name ="Portsection"></a> Configure container to host port mapping</span></span>
<span data-ttu-id="ff370-184">응용 프로그램 매니페스트에 `PortBinding`을 지정하여 컨테이너와의 통신에 사용되는 호스트 포트를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="ff370-185">포트 바인딩은 컨테이너 내에서 서비스가 수신 대기 중인 포트를 호스트의 포트로 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="ff370-186">컨테이너 간 검색 및 통신 구성</span><span class="sxs-lookup"><span data-stu-id="ff370-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="ff370-187">`PortBinding` 요소를 사용하여 컨테이너 포트를 서비스 매니페스트의 끝점에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-187">You can use the `PortBinding` element to map a container port to an endpoint in the service manifest.</span></span> <span data-ttu-id="ff370-188">다음 예제에서 끝점 `Endpoint1`은 고정된 포트 8905를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-188">In the following example, the endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="ff370-189">어떤 포트도 지정하지 않을 수 있는데, 그런 경우 클러스터의 응용 프로그램 포트 범위에서 포트가 무작위로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="ff370-190">게스트 컨테이너의 서비스 매니페스트에서 `Endpoint` 태그를 사용하여 끝점을 지정하는 경우 Service Fabric은 이 끝점을 명명 서비스에 자동으로 게시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="ff370-191">클러스터에서 실행되는 기타 서비스는 해결용 REST 쿼리를 사용하여 이 컨테이너를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

<span data-ttu-id="ff370-192">명명 서비스에 등록하면 [역방향 프록시](service-fabric-reverseproxy.md)를 사용하여 컨테이너 내 컨테이너 간 통신을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-192">By registering with the Naming service, you can perform container-to-container communication within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="ff370-193">역방향 프록시 http 수신 대기 포트와 통신하려는 서비스 이름을 환경 변수로서 제공하면 통신이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="ff370-194">자세한 내용은 다음 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ff370-194">For more information, see the next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="ff370-195">환경 변수 구성 및 설정</span><span class="sxs-lookup"><span data-stu-id="ff370-195">Configure and set environment variables</span></span>
<span data-ttu-id="ff370-196">서비스 매니페스트의 각 코드 패키지에 대해 환경 변수를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-196">Environment variables can be specified for each code package in the service manifest.</span></span> <span data-ttu-id="ff370-197">이 기능은 컨테이너 또는 프로세스 또는 게스트 실행 파일로 배포되는지 여부에 관계 없이 모든 서비스에 대해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="ff370-198">응용 프로그램 매니페스트에 환경 변수 값을 재정의하거나 응용 프로그램 매개 변수로 배포하는 동안 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-198">You can override environment variable values in the application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="ff370-199">다음 서비스 매니페스트 XML 코드 조각은 코드 패키지에 대한 환경 변수를 지정하는 방법의 예제를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-199">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="ff370-200">이러한 환경 변수는 응용 프로그램 매니페스트 수준에서 재정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-200">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="ff370-201">이전 예제에서 `HttpGateway` 환경 변수(19000)에는 명확한 값을 지정했던 반면에 `BackendServiceName` 매개 변수의 값은 `[BackendSvc]` 응용 프로그램 매개 변수를 통해 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-201">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="ff370-202">이렇게 설정하면 응용 프로그램을 배포하고 매니페스트에 고정된 값을 지정하지 않은 경우 `BackendServiceName`에 값을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-202">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="ff370-203">격리 모드 구성</span><span class="sxs-lookup"><span data-stu-id="ff370-203">Configure isolation mode</span></span>

<span data-ttu-id="ff370-204">Windows는 컨테이너 - 프로세스 및 Hyper-V에 대한 두 가지 격리 모드를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="ff370-205">프로세스 격리 모드를 사용하여 동일한 호스트 컴퓨터에서 실행되는 모든 컨테이너는 호스트와 커널을 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-205">With the process isolation mode, all the containers running on the same host machine share the kernel with the host.</span></span> <span data-ttu-id="ff370-206">Hyper-V 격리 모드를 사용하여 커널은 각 Hyper-V 컨테이너와 컨테이너 호스트 간에 격리됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-206">With the Hyper-V isolation mode, the kernels are isolated between each Hyper-V container and the container host.</span></span> <span data-ttu-id="ff370-207">격리 모드는 응용 프로그램 매니페스트 파일의 `ContainerHostPolicies` 태그에서 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-207">The isolation mode is specified in the `ContainerHostPolicies` tag in the application manifest file.</span></span>  <span data-ttu-id="ff370-208">지정될 수 있는 격리 모드는 `process`, `hyperv` 및 `default`입니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-208">The isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="ff370-209">`default` 격리 모드는 Windows Server 호스트에서 `process`로 기본값이 지정되고 Windows 10 호스트에서 `hyperv`로 기본값이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-209">The `default` isolation mode defaults to `process` on Windows Server hosts, and defaults to `hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="ff370-210">다음 코드 조각은 격리 모드가 응용 프로그램 매니페스트 파일에서 지정되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-210">The following snippet shows how the isolation mode is specified in the application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="ff370-211">응용 프로그램 및 서비스 매니페스트에 대한 전체 예제</span><span class="sxs-lookup"><span data-stu-id="ff370-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="ff370-212">예제 응용 프로그램 매니페스트는 다음을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="ff370-213">예제 서비스 매니페스트(이전 응용 프로그램 매니페스트에 지정됨)는 다음을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="ff370-213">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ff370-214">다음 단계</span><span class="sxs-lookup"><span data-stu-id="ff370-214">Next steps</span></span>
<span data-ttu-id="ff370-215">컨테이너화된 서비스를 배포했으므로 [Service Fabric 응용 프로그램 수명 주기](service-fabric-application-lifecycle.md)를 읽고 수명 주기를 관리하는 방법에 대해 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="ff370-215">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="ff370-216">Service Fabric 및 컨테이너 개요</span><span class="sxs-lookup"><span data-stu-id="ff370-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="ff370-217">예제는 [GitHub에서 Service Fabric 컨테이너 코드 샘플](https://github.com/Azure-Samples/service-fabric-dotnet-containers)을 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="ff370-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
